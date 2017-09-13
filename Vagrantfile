# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos72"

  # config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.network :private_network, ip: "192.168.44.38"

  # config.vm.network "public_network"

  # ここはplaybookをマウントさせているので変更しないでください
  config.vm.synced_folder "./playbook", "/vagrant/ansible", :mount_options => ["dmode=775","fmode=664"]

  # [左]ホストのプロジェクトがあるディレクトリ [右]リモートのプロジェクトディレクトリ
  # ホストのパスは自身の環境に合わせて適宜設定してください
  # リモートのパスは"your-project-dir"の部分だけを変更してください
  config.vm.synced_folder "./public_html/your-project-dir", "/var/www/html/your-project-dir"

  config.vm.provider "virtualbox" do |vb|
  #   # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook        = "/vagrant/ansible/site.yml"
    ansible.verbose         = true
    ansible.install         = true
    ansible.limit           = "all" # or only "nodes" group, etc.
    ansible.inventory_path  = "/vagrant/ansible/hosts"
  end
end
