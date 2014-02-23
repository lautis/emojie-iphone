require 'rubygems'
require 'bundler/setup'
require 'json'
require 'gemoji'
require 'fileutils'

IGNORE = ["copyright", "tm"]

# This is UCS-2
def from_code_points(args)
  args.map do |point|
    offset = point - 0x10000
    if point > 0xFFFF
      [0xD800 + (offset >> 10), 0xDC00 + (offset & 0x3FF)].map do |i|
        "\\u#{"%04x" % i}"
      end.join("")
    else
      [point].pack("U")
    end
  end
end

def code_points
  Emoji.send(:mapping).inject({}) do |mapping, (key, unicodes)|
    if unicodes
      mapping[key] = unicodes.map do |str|
        from_code_points(str.chars.map(&:ord)).reduce(:+)
      end
    end
    mapping
  end
end

desc 'Generate JSON of all emoji characters'
task :js do
  output = "emojie = Emojie();\n"
  code_points.each do |image, characters|
    next if IGNORE.include?(image)
    src = "images/emoji/#{image}.png"
    characters.each do |character|
      output << "emojie.register(\"#{character}\", {src: #{src.to_json}});\n"
    end
  end
  File.open("emojie-iphone.js", "w:utf-8") { |f| f.write(output) }
end

task :images do
  FileUtils.rm Dir.glob("images/emoji/*")
  (Emoji.names - Emoji.custom).each do |emoji|
    FileUtils.copy(File.join(Emoji.images_path, "emoji", "#{emoji}.png"), File.join("images", "emoji", "#{emoji}.png"))
  end
end
