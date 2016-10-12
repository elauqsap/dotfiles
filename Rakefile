CWD=File.expand_path(File.dirname(__FILE__))

desc "Update dotfiles to most recent version"
task :update do
  puts "pulling latest from repo"
  system "cd #{CWD} && git pull origin master"
  system "cd #{CWD} && git submodule update --recursive"
  replace_files
  setperms
end

desc "Set permissions - take away perms from group and other"
task :setperms do
  puts "setting permissions"
  setperms
end

def replace_files
  files = [
    '.vim',
    '.vimrc',
    '.gvimrc',
    '.zshrc',
    '.fonts',
		'.tmux',
		'.tmux.conf',
  ]
  files.each do |file|
    system "rm -rf #{ENV['HOME']}/#{file}"
  end

  link_file("#{CWD}/zsh/_zshrc", "#{ENV['HOME']}/.zshrc")
  link_file("#{CWD}/tmux/_tmux.conf", "#{ENV['HOME']}/.tmux.conf")
  link_file("#{CWD}/tmux", "#{ENV['HOME']}/.tmux")
  link_file("#{CWD}/vim/_vimrc", "#{ENV['HOME']}/.vimrc")
  link_file("#{CWD}/vim/_gvimrc", "#{ENV['HOME']}/.gvimrc")
  link_file("#{CWD}/vim", "#{ENV['HOME']}/.vim")
end

def link_file(src, target)
  system "ln -fs #{src} #{target}"
end

def setperms
  system "chmod -R g-rwx,o-rwx #{CWD}"
end
