ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'
 
Vagrant.configure("2") do |config|
 
 	config.vm.define "docker-4-newman" do |m|
		
		m.vm.provider "docker" do |d|	
			d.name = 'docker-4-newman'
			
			d.force_host_vm = true
			d.has_ssh = true
			
		    
			d.image = "postman/newman_ubuntu1404" 
			#d.volumes = ["/home/vagrant/src/newman-with-docker-on-windows:/vagrant/newman-with-docker-on-windows"]
			d.volumes = ["/home/vagrant/src:/vagrant/newman-with-docker-on-windows"]
			d.cmd = ["run", "/vagrant/newman-with-docker-on-windows/GOOGLE.postman_collection.json", "--environment=/vagrant/newman-with-docker-on-windows/GOOGLE_ENV.postman_environment.json", "--reporters", "cli,junit,html", "--reporter-junit-export", "/vagrant/newman-with-docker-on-windows/newman-report.xml", "--reporter-html-export", "/vagrant/newman-with-docker-on-windows/outputfile.html" ]
			
			d.vagrant_machine = "dockerhostvm"
			
			#d.vagrant_vagrantfile = "C:/work/projects/opensource/github.com.melissapalmer/DockerHostVagrantfile"
			#include DockerHostVagrantfile from same folder in GIT project to be shareable with others
			d.vagrant_vagrantfile = "DockerHostVagrantfile"
		end
	end
end