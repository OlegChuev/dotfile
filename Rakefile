desc "Setup mandatory applications using Homebrew"
task :install_apps do
  puts "Installing mandatory apps using Homebrew..."
  system("brew bundle --file=./Brewfile")
  puts "Installation complete!"
end

desc "Symlink dotfiles to the home directory"
task :setup_dotfiles do
  dotfiles = Dir.glob(File.join(Dir.pwd, "dotfiles", ".*")).select { |f| File.file?(f) && File.basename(f) != ".git" }
  
  dotfiles.each do |dotfile|
    target = File.join(Dir.home, File.basename(dotfile))

    unless File.exist?(target)
      File.symlink(dotfile, target)
      puts "Symlinked #{dotfile} to #{target}"
    else
      puts "Skipped #{target}, already exists"
    end
  end
end

desk "Make Orbstack as a default Docker Desktop Alternative"
task :setup_docker_env do 
  system("docker context use orbstack")
end

desc "Full setup: Install apps and set up dotfiles"
task :setup => [:install_apps, :setup_dotfiles, :setup_docker_env]
