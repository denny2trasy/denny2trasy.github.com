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
  system 'git add --all'
  system "git commit -m '#{args.desc}'"
  system "git push origin source"
  puts "**************************************************"
  puts "2 - Copy new site code to backup place"
  system 'cp -aR _site/ ../../liguande/site'
  puts "**************************************************"
  puts "3 - Change branch to master"
  system 'git co master'
  system "cp -aR ../../liguande/site/ ."
  puts "**************************************************"
  puts "4 - Summit new site to master branch"
  system "git add -all"
  system "git commit -m '#{args.desc}'"
  system "git push origin master"
end