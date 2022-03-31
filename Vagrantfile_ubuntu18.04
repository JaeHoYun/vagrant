Vagrant.configure("2") do |config|

  # vagrant plugin install vagrant-disksize 설치
  # vagrant plugin install vagrant-vbguest 설치
  # vagrant plugin install vagrant-hosts 설치 불필요
  # vagrant up 실행 시 default:SSH auth method: private key  에서 타임아웃 발생 시 아래와 같이 설정
  # config.ssh.insert_key = false
  
  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "node02"
  config.disksize.size = "20GB"
  config.vm.box_check_update = false
  
  # NAT
  # config.vm.network "public_network" 퍼블릭 네트워크 명시적 선언하지 않아도 기본적으로 adapter 1 에 NAT 할당
  # VM NAT. 모든 VM 이 10.0.2.15 기본 할당. 모든 포트 포워딩은 기본적으로 adaptet 1 / NAT 에 적용
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  # host-only Network
  # 192.168.56.1xx 대역으로만 설정 가능, 그 외엔 vagrant up 중 에러 발생 (NDIS6 관련 트러블슈팅으로 해결 불가능)
  config.vm.network "private_network", ip: "192.168.56.111"
  
  # Bridged Network
  # 내 공유기 네트워크 대역에서 IP 자동 할당.
  # bridge: 에 공유기와 연결된 내 데스크탑의 네트워크 아답터 이름 확인 후 입력
  config.vm.network "public_network", bridge: "Intel(R) Ethernet Connection I217-V"
  
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "node2"
    vb.memory = "2048"
	  vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
	  sudo apt-get upgrade -y
	  sudo apt-get dist-upgrade -y
	  sudo apt-get install -y openssh
	  sudo apt-get autoremove -y
  SHELL
end
