
open /j/tmp25/cpuinfo-tiny.txt | parse -r '(?P<value>(.|\n)*?)\n\n' | each { echo $it.value | lines | parse -r '(?P<name>.*?)\s*:\s*(?P<value>.*)' }
