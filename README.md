
Configuration of Logstash 
=============================
To Modify the the remoting Host IP from Input (logstash.config)
It will migrate data to local's elasticsearch

	input {
	  elasticsearch {
	    hosts => "192.168.1.1:9200"
	 	index => "*" 
	 	docinfo => true
	  }
	}

	output {
	  elasticsearch { hosts => ["es-server:9200"] 
	   index => "%{[@metadata][_index]}"
	    document_type => "%{[@metadata][_type]}"
	    document_id => "%{[@metadata][_id]}"
	   }
	  
	}



Docker Command
=============================

### To pull the docker images
	docker pull logstash

### To run the container with .config
	docker run -it -v $PWD:/config-dir  logstash:latest -f /config-dir/logstash.config

$PWD is folder from host.
/config-dir is folder from container.
-v is volume flag for mounting.





