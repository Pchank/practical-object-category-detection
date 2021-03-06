name = practical-category-detection-2014a
DST = vgg@login.robots.ox.ac.uk:WWW/share
DSTDOC = vgg@login.robots.ox.ac.uk:WWW/practicals/category-detection

.PHONY: prepack, pack, pack-data, pack-code, post, clean, distclean

pack-all: pack-data pack-code pack

code=\
boxinclusion.m \
boxoverlap.m \
boxsuppress.m \
detect.m \
detectAtMultipleScales.m \
evalDetections.m \
evaluateModel.m \
exercise1.m \
exercise2.m \
exercise3.m \
exercise4.m \
exercise5.m \
extract.m \
loadData.m \
setup.m \
README.md \
vlfeat \
matconvnet

doc=\
doc/images \
doc/instructions.html

data=\
data/signs.mat \
data/signs-sample-image.jpg \
data/signs

code:=$(addprefix $(CURDIR)/,$(code))
data:=$(addprefix $(CURDIR)/,$(data))
deps:=$(shell find $(code) $(doc) $(data) -type f | sed "s/ /\\\\ /g")

pack: data/$(name).tar.gz
pack-data: data/$(name)-data-only.tar.gz
pack-code: data/$(name)-code-only.tar.gz

data/$(name).tar.gz: $(deps)
	rm -rf data/$(name)
	mkdir -p data/$(name)/{doc,data}
	ln -sf $(data) data/$(name)/data/
	ln -sf $(doc) data/$(name)/doc/
	ln -sf $(code) data/$(name)/
	tar -C data -czvhf data/$(name).tar.gz $(name)/

data/$(name)-data-only.tar.gz: $(deps)
	rm -rf data/$(name)
	mkdir -p data/$(name)/{doc,data}
	ln -sf $(data) data/$(name)/
	tar -C data -czvhf data/$(name)-data-only.tar.gz $(name)/

data/$(name)-code-only.tar.gz: $(deps)
	rm -rf data/$(name)
	mkdir -p data/$(name)/{doc,data}
	ln -sf $(doc) data/$(name)/doc/
	ln -sf $(code) data/$(name)/
	tar -C data -czvhf data/$(name)-code-only.tar.gz $(name)/

post-doc:
	rsync -rvt doc/images $(DSTDOC)/
	rsync -vt doc/instructions.html $(DSTDOC)/index.html

post: pack-all
	rsync -vt data/$(name).tar.gz $(DST)/
	rsync -vt data/$(name)-data-only.tar.gz $(DST)/
	rsync -vt data/$(name)-code-only.tar.gz $(DST)/

clean:
	find . -name '*~' -delete

distclean: clean
	rm -f data/$(name)*.tar.gz
