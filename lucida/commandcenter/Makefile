all: thrift

thrift:
	@if [ ! -d "lucidaservice" ]; then \
		thrift --gen py ../lucidaservice.thrift; \
		thrift --gen py ../lucidatypes.thrift; \
		cd gen-py; \
		mv * ..; \
		cd ..; \
		rmdir gen-py; \
		rm __init__.py; \
	fi

clean:
	rm -rf lucidaservice lucidatypes

start_server: 
	gnome-terminal -x bash -c "python app.py $(filter-out $@,$(MAKECMDGOALS)); read -n1"

docker:
	cp ../lucidaservice.thrift .; \
	cp ../lucidatypes.thrift .; \
	docker build -t lucida_cmd .; \
	rm lucidaservice.thrift; \
	rm lucidatypes.thrift;

.PHONY:	all venv thrift clean start_server docker
