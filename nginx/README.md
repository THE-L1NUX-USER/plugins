# Nginx Plugin
                                                                                              
## Prerequisites

- Download and install the latest version of the [Site24x7 Linux agent] (https://www.site24x7.com/app/client#/admin/inventory/add-monitor) in the server where you plan to run the plugin. 

#### Enable nginx_status to get metrics -

1. Open terminal and run the following command to open NGINX server configuration file.
		 ``` 
		 $sudo vi /etc/nginx/nginx.conf 
		 ```
2. Add the following code inside the server block which is present in the "/etc/nginx/nginx.conf" file.
```
location /nginx_status {
    stub_status;
    	
}
```
3. Save and close the /etc/nginx/nginx.conf file.
4. Now restart the nginx to apply the changes :
```bash
sudo systemctl reload nginx
```


## Plugin Installation  

- Once installed the respective agent in the server, create a directory named "nginx".
      
- Download all the files in the "nginx" folder and place it under the "nginx" directory.

		wget https://raw.githubusercontent.com/site24x7/plugins/master/nginx/nginx.py
		wget https://raw.githubusercontent.com/site24x7/plugins/master/nginx/nginx.cfg

- Execute the below command with appropriate arguments to check for the valid json output:

 ```bash
 python3 nginx.py --nginx_status_url=<nginx stats url> --username=<nginx username> --password=<nginx password> 
 ```

- Once the above command execution given the valid json, further provide the command argument as configurations in nginx.cfg file.
```
  [nginx]
  plugin_version=1
  heartbeat=true
  nginx_status_url="http://localhost/nginx_status"
  username=None
  password=None
  timeout=60
  logs_enabled = "true"
  log_type_name = "Nginx Logs"
  log_file_path = "/var/log/nginx/access*"
```	
- Once the configuration done, move the "nginx" directory under the Site24x7 Linux Agent plugin directory: 

		``` Linux             ->   /opt/site24x7/monagent/plugins/nginx ```

		
The agent will automatically execute the plugin within five minutes and send performance data to the Site24x7 data center.

In case if user needs to run this nginx plugin in windows server, please follow the steps in below link.
https://support.site24x7.com/portal/en/kb/articles/run-python-plugin-scripts-in-windows-servers


## Supported Metrics

- **Currently active client connections**

    Current active client connections including waiting connections

- **Number of connections where nginx is reading the request header**

    The current number of connections where nginx is reading the request header

- **Number of connections where nginx is writing the response back to the client**

    The current number of connections where nginx is writing the response back to the client

- **Number of idle client connections waiting for a request**

    The current number of idle client connections waiting for a request
- **Count of client requests**

    Client request count in nginx

- **Count of successful client connections**

    Successful client connection in nginx

- **Count of dropped connections**

    Dropped connections count








