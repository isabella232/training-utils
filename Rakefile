require 'fileutils'

task default: :install

task :install do
  scripts = Dir['*'] - %w{LICENSE.txt Rakefile README.md}
  target  = ENV["TARGET"] || ask_for_target_dir
  File.directory?(File.expand_path(target)) or abort("Install directory isn't a directory")

  scripts.each do |f|
    puts "  Linking #{target}/#{f}"
    path_to_target = File.expand_path(target)
    if File.exist?(path_to_target) && File.symlink?(path_to_target)
      FileUtils.rm(path_to_target)
    end
    FileUtils.symlink File.absolute_path(f), path_to_target
  end
end

def ask_for_target_dir
  puts "Directory to install? (needs to be in your $PATH, /usr/local/bin is the default) "
  answer = STDIN.gets.chomp
  (answer unless answer == "") || "/usr/local/bin"
end
