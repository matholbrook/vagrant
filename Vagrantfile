# Vagrant on AWS provisioning

tstamp = `date +%s`
host   = `hostname`

Vagrant.configure("2") do |config|
  config.vm.box     = "dummy"
  config.vm.box.url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
  config.vm.synced_folder "." "/vagrant", disabled: true
  config.vm.provider :aws do |aws, override|
  
    # configure these five ENV VAR's in ~/.bashrc so not tied to one user
    aws.access_key_id             = ENV['AWS_ACCESS_KEY']
    aws.secret_access_key         = ENV['AWS_SECRET_KEY']
    aws.keypair_name              = ENV['AWS_KEYNAME']
    override.ssh.private_key_path = ENV['AWS_KEYPATH']
    aws.tags = {'Name' => "Vagrant_#{ENV['INITIALS']}_#{host}_#{tstamp}"}
    aws.block_device_mapping      = [
                                     {'DeviceName'              => '/dev/sda1',
                                      'Ebs.VolumeSize'          => 10,     # size in GB
                                      'Ebs.VolumeType'          => 'gp2',  #  SSD
                                      'Ebs.DeleteOnTermination' => 'true'}
                             #       {'DeviceName'              => '/dev/sdb',
                             #         Ebs.VolumeSize'          => 15,     # size in GB
                             #         Ebs.VolumeType'          => 'gp2',  # SSD
                             #         Ebs.DeleteOnTermination' => 'true'}
                                    ]
    

end
