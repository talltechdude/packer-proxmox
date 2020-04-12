
#!make
include .env
export

http/preseed.cfg:
	mkdir -p http
	set -a

	password_hash1=$$(mkpasswd -R 1000000 -m sha-512 ${ssh_password}) \
	j2 preseed.cfg.j2 > http/preseed.cfg

.PHONY: clean all

.PHONY: build
build: http/preseed.cfg
	mkdir -p playbook/logs
	ansible-galaxy install --force -p playbook/roles -r playbook/requirements.yml
	packer build --var-file config.json debian-10.json

all: http/preseed.cfg build

clean:
	rm -f "http/preseed.cfg"
