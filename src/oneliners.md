
echo "blue : green" | parse -r '(?P<name>.*?)\s*:\s*(?P<value>.*)'

open /j/tmp25/nushelltmp/data/cpuinfo-tiny.txt | parse -r '(?P<value>(.|\n)*?)\n\n' | each { echo $it.value | lines | parse -r '(?P<name>.*?)\s*:\s*(?P<value>.*)' }

### Regex References

https://www.janmeppe.com/blog/regex-for-noobs/

https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285

https://www.regular-expressions.info/optional.html

https://stackoverflow.com/questions/7988942/what-does-this-django-regex-mean-p
