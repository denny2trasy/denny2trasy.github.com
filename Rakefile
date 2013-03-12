#1.git pull origin source
#2.copy _site to backup
#3.git co master
#4.copy backup to master branch
#5.git pull origin master
# run this task with bollow code
# => noglob rake submit_my_posts["blablala"]
task :submit_my_posts,[:desc] do |t, args|
  puts "#{args.desc}"
  puts "**************************************************"
  puts "1 - Summit new code to source branch"
  system 'git co source'
  system 'git pull origin source'
  system 'git add --all'
  system "git commit -m '#{args.desc}'"
  system "git push origin source"
  puts "**************************************************"
  puts "2 - Copy new site code to backup place"
  system 'cp -aR _site/ ../denny2trasy_master/'
  puts "**************************************************"
  puts "3 - Change dir to denny2trasy_master"
  system 'cd ../denny2trasy_master'
  puts "**************************************************"
  puts "4 - Summit new site to master branch"
  system "git co master"
  system "git pull origin master"
  system "git add --all"
  system "git commit -m '#{args.desc}'"
  system "git push origin master"
end