# Steps to configure logstash

1. **Download logstash from here**
[logstash](https://www.elastic.co/downloads/logstash)

2. **Set logstash home into environment path**

    - **ubuntu**

        export LOGSTASH_HOME=/home/pradeep/logstash-5.2.1

        export PATH=$PATH:$LOGSTASH_HOME/bin

        > append above lines into bashrc file if you want to configure it for permanently.

    - **windows**

        - From the desktop, right click the Computer icon.
        - Choose Properties from the context menu.
        - Click the Advanced system settings link.
        - Click Environment Variables.
        - In the section System Variables.
        - Create new variable

            name  : LOGSTASH_HOME

            value : /home/pradeep/logstash-5.2.1
        - Find the PATH environment variable and select it. Click Edit. If the PATH environment variable does not exist, click New.
        - Append above **LOGSTASH_HOME** into PATH variable like **;%LOGSTASH_HOME%**

3. **Run logstash**

    ```
    pradeep@xe-tlindual-parya:~$ logstash -e 'input { stdin { } } output { stdout { } }'
    Sending Logstash's logs to /mnt/Xebia/elk/software/logstash-5.2.1/logs which is now configured via log4j2.properties
    The stdin plugin is now waiting for input:
    [2017-02-19T15:21:58,754][INFO ][logstash.pipeline        ] Starting pipeline {"id"=>"main", "pipeline.workers"=>4, "pipeline.batch.size"=>125, "pipeline.batch.delay"=>5, "pipeline.max_inflight"=>500}
    [2017-02-19T15:21:58,764][INFO ][logstash.pipeline        ] Pipeline main started
    [2017-02-19T15:21:58,858][INFO ][logstash.agent           ] Successfully started Logstash API endpoint {:port=>9600}
    hello logstash
    2017-02-19T09:52:04.828Z xe-tlindual-parya hello logstash
    [2017-02-19T15:22:06,790][WARN ][logstash.agent           ] stopping pipeline {:id=>"main"}
    ```
    > **logstash -e 'input { stdin { } } output { stdout { } }'** will take input from standard input i.e. console and put forward it to standard output i.e. again console.

    > **To read data from different locations we need to configure filebeat, that read data from particular location and forward it to logstash**


4. **Download filebeat from here** [filebeat](https://www.elastic.co/downloads/beats/filebeat)
5. **Getting started with filebeat** [filebeat](https://www.elastic.co/guide/en/beats/filebeat/5.2/filebeat-getting-started.html)
6. **Configure file filebeat input** location and output location in filebeat.yml file located in downloaded filebeat folder.


    ```
    - input_type: log

      # Paths that should be crawled and fetched. Glob based paths.
      paths:
        - /home/pradeep/logs/*.log

    output.logstash:
      # The Logstash hosts
      hosts: ["localhost:5043"]
    ```
7. **Create logstash pipeline**
    - **create a file name <FILE_NAME>.conf (**first-pipeline.conf**) and put following content in that :**
    ```
    input {
    	beats {
            port => "5043"
        }
    }
    filter {
        grok {
            match => { "message" => "%{COMBINEDAPACHELOG}"}
        }
        geoip {
            source => "clientip"
        }
    }
    output {
    	stdout { codec => rubydebug }
    }
    ```

8. **verify configuration**
    ```
    pradeep@xe-tlindual-parya:$ logstash -f first-pipeline.conf --config.test_and_exit
    Sending Logstash's logs to /home/pradeep/elk/software/logstash-5.2.1/logs which is now configured via log4j2.properties
    Configuration OK
    [2017-02-26T19:23:08,492][INFO ][logstash.runner          ] Using config.test_and_exit mode. Config Validation Result: OK. Exiting Logstash
    pradeep@xe-tlindual-parya:$

    ```

7. **start logstash**
    ```
    logstash -f first-pipeline.conf --config.reload.automatic
    ```

8. **start filebeat**
    ```
    filebeat -e -c filebeat.yml -d "publish"
    ```

9. **filebeat to force start**

    > Filebeat stores the state of each file it harvests in the registry, deleting the registry file forces Filebeat to read all the files it’s harvesting from scratch.

    ```
    rm data/registry
    ```



