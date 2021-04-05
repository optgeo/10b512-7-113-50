require 'json'
require 'find'

CONFIG = JSON.parse(`parse-hocon global.conf`)

desc 'host the site'
task :host do
  sh "budo -d docs"
end

desc 'copy tiles'
task :copy do
  9.upto(13) {|z|
    Find.find("../10b512/docs/zxy/#{z}") {|path|
      next unless /\/(\d*)\/(\d*).webp$/.match path
      x, y = [$1, $2].map{|v| v.to_i }
      x7 = x >> (z - 7)
      y7 = y >> (z - 7)
      next unless x7 == 113 && y7 == 50
      print "#{z}/#{x}/#{y} -> 7/#{x7}/#{y7}\n"
      sh "mkdir -p docs/zxy/#{z}/#{x}"
      sh "cp #{path} docs/zxy/#{z}/#{x}"
    }
  }
end

desc 'build style.json'
task :style do
  sh "parse-hocon style.conf > docs/style.json"
  sh "gl-style-validate docs/style.json"
end

