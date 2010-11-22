desc "Release a new version"
task :release do
  raise "set VERSION=x.x.x" unless ENV['VERSION']
  
  new_version = "version: #{ENV['VERSION']} (#{Time.now.strftime('%m/%d/%Y')})"
  
  ['ops-theme.html'].each do |file|
    new_file = File.read(file).gsub(/version:.*/, new_version)
    File.open(file, 'w') { |f| f.write(new_file) }
    
    unless File.read(file).index(new_version)
      raise "#{file} does not contain: #{new_version}"
    end
  end
  
  `git commit -a -m "Release v#{ENV['VERSION']}"`
  `git push origin master`
  
  `git tag "v#{ENV['VERSION']}"`
  `git push --tags`
end