# Copyright © 2015 Jakub Wilk <jwilk@jwilk.net>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the “Software”), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

.PHONY: all
all:

.PHONY: clean
clean:
	rm -rf *.zip tmp* moo* zoo*

ifeq "$(shell which zip)" ""
$(error zip(1) is needed to create zip samples)
endif

all: absolute1.zip
absolute1.zip:
	umask 022 && echo moo > mooooooo
	zip -X -m $(@) mooooooo
	sed -i -e s,mooooooo,/tmp/moo, $(@)

all: absolute2.zip
absolute2.zip:
	umask 022 && echo moo > moooooooo
	zip -X -m $(@) moooooooo
	sed -i -e s,moooooooo,//tmp/moo, $(@)

all: relative0.zip
relative0.zip:
	mkdir -m 755 tmp
	umask 022 && echo moo > moo
	cd tmp && zip -X ../$(@) ../moo
	rm -rf tmp moo

all: relative2.zip
relative2.zip:
	mkdir -p -m 755 tmp/tmp
	umask 022 && echo moo > moo
	cd tmp && zip -X ../$(@) tmp/../../moo
	rm -rf tmp moo

all: symlink.zip
symlink.zip:
	ln -sf /tmp/moo moo
	zip -X -y -m $(@) moo
	umask 022 && echo moo > zoo
	zip -X -m $(@) zoo
	sed -i -e s/zoo/moo/ $(@)

all: dirsymlink.zip
dirsymlink.zip:
	ln -sf /tmp tmp
	zip -X -y -m $(@) tmp
	mkdir -m 755 tmp
	umask 022 && echo moo > tmp/moo
	zip -X $(@) tmp/moo
	rm -rf tmp


# vim:ts=4 sts=4 sw=4 noet
