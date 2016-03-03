SHELL = /bin/bash

.PHONY: all
all: python2.7/venv python2.7/sum.so
all: python3.5/venv python3.5/sum.so

%/venv:
	set -ex; \
	PYTHON=$$(grep -Eo '^[^/]+' <<< $@); \
	mkdir -p $$PYTHON; \
	virtualenv $@ -p $$PYTHON

%/sum.so: sum.c
	set -ex; \
	PYTHON=$$(grep -Eo '^[^/]+' <<< $@); \
	mkdir -p $PYTHON; \
	PYTHON=$$(sed s/python/python-/ <<< $$PYTHON); \
	gcc -Wall -fPIC -shared $$(pkg-config --cflags --libs $$PYTHON) -o $@ $<

.PHONY: clean
clean:
	rm -rf python2.7 python3.5