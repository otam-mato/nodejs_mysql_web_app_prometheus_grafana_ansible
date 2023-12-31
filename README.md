# Node.JS + MySQL Web App.<br><br>Setting up monitoring of the default metrics with Prometheus and Grafana. <br><br> Ansible deployment.

<br>

> **Note:** The part of a series of demo projects in which I manipulate a Node.js application using various technologies.<br>
>
> The app built using Node.js and Express, originally presented at this [GitHub Repository](https://github.com/otam-mato/nodejs_mysql_web_app_terraform.git).
>
> In the current installment, I am setting up monitoring of the app with Prometheus and Grafana.
>
> Previous deployment of the same stack with **Docker-compose** available at this [GitHub Repository](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana.git).
>
> This time, I am using **Ansible**.
<br>

## Deployment Strategy

1. **Prometheus and Grafana Deployment:**
   We will use the Ansibe and pull images of Prometheus and Grafana from DockerHub
   
2. **Node.js:**
   We include the task in Ansible playbook to build the app container image from a Docker file

<br>

## Architecture Diagram

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana_ansible/assets/113034133/052ceeb8-cdef-4d83-8f84-e645374472a3" width="800px"/>
</p>

<br>


## Technologies used
- **Prometheus**
- **Grafana**
- **Node.JS**
- **Express**
- **JavaScript**
- **MySQL**
- **Docker**
- **AWS**
- **EC2**
- **Ansible**
<br>

## Functionality

This web application interfaces with a MySQL database, facilitating CRUD (Create, Read, Update, Delete) operations on the database records. Monitoring is implemented via **Prometheus** and **Grafana**.

**<details markdown=1><summary markdown="span">Detailed app description</summary>**

## Summary

The app sets up a web server for a supplier management system. It allows viewing, adding, updating, and deleting suppliers. 

#### **Dependencies and Modules**:
   - **express**: The framework that allows us to set up and run a web server.
   - **body-parser**: A tool that lets the server read and understand data sent in requests.
   - **cors**: Ensures the server can communicate with different web addresses or domains.
   - **mustache-express**: A template engine, letting the server display dynamic web pages using the Mustache format.
   - **serve-favicon**: Provides the small icon seen on browser tabs for the website.
   - **Custom Modules**: 
     - `supplier.controller`: Handles the logic for managing suppliers like fetching, adding, or updating their details.
     - `config.js`: Keeps the server's settings for connectind to the MySQL database.

#### **Configuration**:
   - The server starts on a port taken from a setting (like an environment variable) or uses `3000` as a default.

#### **Middleware**:
   - It's equipped to understand data in JSON format or when it's URL-encoded.
   - It can chat with web pages hosted elsewhere, thanks to CORS.
   - Mustache is the chosen format for web pages, with templates stored in a folder named `views`.
   - There's a public storage (`public`) for things like images or stylesheets, accessible by anyone visiting the site.
   - The site's tiny browser tab icon is fetched using `serve-favicon`.

#### **Routes (Webpage Endpoints)**:
   - **Home**: `GET /`: Serves the home page.
   - **Supplier Operations**: 
     - `GET /suppliers/`: Fetches and displays all suppliers.
     - `GET /supplier-add`: Serves a page to add a new supplier.
     - `POST /supplier-add`: Receives data to add a new supplier.
     - `GET /supplier-update/:id`: Serves a page to update details of a supplier using its ID.
     - `POST /supplier-update`: Receives updated data of a supplier.
     - `POST /supplier-remove/:id`: Removes a supplier using its ID.

#### **Starting Up**:
   - The server comes to life, starts listening for visits, and announces its awakening with a log message.

</details>

**<details markdown=1><summary markdown="span">Prometheus details</summary>**

Prometheus is an open-source monitoring and alerting toolkit designed for reliability and scalability. It is part of the Cloud Native Computing Foundation (CNCF) and is widely used in the field of cloud-native and containerized applications. Prometheus is used for collecting, storing, and querying metrics and other essential data generated by various software systems.

Key features and components of Prometheus include:

1. **Data Collection**: Prometheus scrapes metrics from instrumented jobs, services, and applications at regular intervals. It supports multiple data formats, including a simple text-based format and more efficient binary formats.

2. **Data Storage**: Collected data is stored in a time-series database optimized for fast querying and aggregations. The database can be configured to retain data for a specified time.

3. **Query Language**: Prometheus Query Language (PromQL) allows users to write powerful queries to aggregate, transform, and process data for monitoring and alerting purposes.

4. **Alerting**: Prometheus supports alerting based on defined alerting rules. Alerts can be configured to notify operators or integrate with notification systems like Alertmanager.

5. **Scalability**: Prometheus is designed to be horizontally scalable, and it supports federated setups to collect and aggregate data from multiple Prometheus instances.

6. **Visualization**: While Prometheus itself doesn't provide visualization capabilities, it integrates well with other tools like Grafana for creating dashboards and visualizing data.

7. **Exporters**: Prometheus exporters are small applications or libraries that allow you to monitor various third-party systems, services, and components. Many popular software components have Prometheus exporters available.

Prometheus is often used in combination with other technologies such as Grafana for visualization and Alertmanager for alert management. It's especially popular in containerized and microservices-based environments, helping operators and developers monitor and troubleshoot complex, dynamic systems.

</details>

**<details markdown=1><summary markdown="span">Grafana details</summary>**

Grafana is an open-source, multi-platform analytics and monitoring platform designed to integrate with various data sources and provide advanced visualization, alerting, and exploration capabilities. It is commonly used in conjunction with time-series databases and monitoring systems, including Prometheus, InfluxDB, Elasticsearch, and more. Grafana allows users to create interactive and customizable dashboards to gain insights from their data.

Key features of Grafana include:

1. **Data Source Integration**: Grafana supports a wide range of data sources, including time-series databases (Prometheus, InfluxDB, Graphite), relational databases (MySQL, PostgreSQL), cloud services (AWS CloudWatch, Google Cloud Monitoring), and more. This versatility allows users to consolidate data from different systems in a single dashboard.

2. **Dashboard Creation**: Users can create dashboards to visualize and explore data through a web-based interface. Grafana offers a drag-and-drop dashboard builder with various panel types for different visualizations, such as graphs, tables, and maps.

3. **Data Querying**: Grafana provides an SQL-like query language for retrieving and manipulating data from data sources. Users can fine-tune queries and create custom transformations.

4. **Alerting**: Grafana supports alerting based on data queries and conditions. Users can configure thresholds and alert notifications, including email, Slack, and other channels, through integration with notification systems.

5. **Templating**: Templating enables the creation of dynamic dashboards. Variables can be used in queries and allow for easy switching between different data sources or filtering data.

6. **User and Team Management**: Grafana includes user authentication, role-based access control, and team management features, making it suitable for multi-user and collaborative environments.

7. **Plugins and Extensibility**: Grafana's plugin system allows for custom panels, data sources, and apps to be developed and integrated into the platform. This extensibility makes it adaptable to various use cases.

8. **Community and Community-Driven Development**: Grafana has an active and engaged open-source community, which results in frequent updates, a wide range of plugins, and community-contributed resources.

Grafana is widely used by DevOps, system administrators, and data analysts for monitoring infrastructure, applications, and services. It has become a standard tool for creating interactive, real-time dashboards that help users understand and respond to the performance and health of their systems.

</details>

<br>

## Prerequisites

- A work station or an **EC2** instance.
  
- Install **Node.js**, **npm**, and **Git**
   
- Install **Ansible** and **Docker**

  **<details markdown=1><summary markdown="span">click for details</summary>**
  
   **RHEL:**
  
   ```
   sudo yum install python3-pip python3-devel gcc
   ```
   ```
   sudo pip3 install ansible
   ```
   ```
   sudo yum install -y docker
   ```
   ```
   sudo systemctl start docker
   ```
   ```
   sudo usermod -aG docker $USER
   ```
   
   **Ubuntu 22.04 :**

   ```
   sudo apt-get install ansible
   ```
   ```
   ansible-galaxy collection install community.docker
   ```
   ```
   sudo apt install python3-pip
   ```
   ```
   sudo pip3 install docker
   ```
   ```
   sudo usermod -aG docker $USER
   ```

  </details>

<br>

## Implementation

Follow these steps for successful implementation:

1. [**Modify the app files to allow Prometheus collecting metrics.**](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/blob/main/README.md#1-modify-the-app-files-to-allow-prometheus-collecting-metrics)
2. [**Create the configuration file for Prometheus"prometheus.yml".**](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/blob/main/README.md#2-create-the-configuration-file-for-prometheusprometheusyml)
4. [**Create the configuration file for Grafana "datasources.yml."**](https://github.com/otam-mato/nodejs_elk/blob/main/README.md#3-launch-the-elk-stack-with-this-docker-compose-file)
5. [**Create the Ansible playbook "ansible-deploy-containers.yml".**](https://github.com/otam-mato/nodejs_ansible/blob/main/README.md#4-create-the-ansible-playbook-ansible-deploy-containersyml)
7. [**Run the Ansible playbook "ansible-deploy-containers.yml" file.**](https://github.com/otam-mato/nodejs_ansible/blob/main/README.md#5-run-the-ansible-playbook-ansible-deploy-containersyml-file)

<br>

## Screenshots

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/41b3ff50-2ef2-44f7-9bbf-eb8f875305dd" width="700px"/>
</p>


<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/0a7f8661-2b55-476b-8227-aac39c578c8a" width="700px"/>
</p>

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/8d851dd0-5c0f-424c-9cca-344ab1072aed" width="700px"/>
</p>

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/0dba5508-e41e-46ee-9159-446dcf2ffa75" width="700px"/>
</p>

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/d18c55d1-30e3-4a0c-8c94-a4fc6f70df09" width="700px"/>
</p>

<br>

## Steps

### 1. Modify the app files to allow Prometheus collecting metrics

- [**package.json**](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana_ansible/blob/1b3fbeafdfc4e3d4ec0eb21333c172a62d20247d/web_app_files/containers/node_app/codebase_partner/package.json)

  **<details markdown=1><summary markdown="span">click for details</summary>**

  ![image](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/0f1ff0c1-72fb-4f5c-8486-7740b062867b)

  </details>
  
- [**index.js**](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana_ansible/blob/1b3fbeafdfc4e3d4ec0eb21333c172a62d20247d/web_app_files/containers/node_app/codebase_partner/index.js)

  **<details markdown=1><summary markdown="span">click for details</summary>**

  ![image](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/b33de535-5449-4571-8463-7f51741cd835)

  </details>

### 2. Create the configuration file for Prometheus"prometheus.yml". 

- [**prometheus.yml**](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana_ansible/blob/1b3fbeafdfc4e3d4ec0eb21333c172a62d20247d/web_app_files/containers/node_app/prometheus/prometheus.yml)

  It will be pulled into the Prometheus container during its creation using Docker-compose.
  
### 3. Create the configuration file for Grafana "datasources.yml". 

- [**datasources.yml**](https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana_ansible/blob/1b3fbeafdfc4e3d4ec0eb21333c172a62d20247d/web_app_files/containers/node_app/grafana/datasources.yml)

  It will be pulled into the Grafana container during its creation using Docker-compose.

### 4. Create the Ansible playbook "ansible-deploy-containers.yml".

- [**ansible-deploy-containers.yml**](https://github.com/otam-mato/nodejs_ansible/blob/86631bd672ee8045966b51c6326a03fe6e9ca3fa/ansible-deploy-containers.yml)

  **<details markdown=1><summary markdown="span">click for details</summary>**

  This Ansible playbook is designed to deploy Docker containers for Prometheus, Grafana, and a Node.js application. It creates Docker networks, volumes, and starts the containers accordingly.

   Here's a breakdown of the playbook:
   
   1. **Docker Network Creation**
   - Creates a Docker network named `my-network` using the `docker_network` module.
     
   2. **Docker Volume Creation**
   - Creates Docker volumes for Prometheus and Grafana data separately using the `docker_volume` module.
   
   3. **Start Prometheus Container**
   - Starts a Prometheus container with the following configurations:
     - **Name**: `prometheus`
     - **Image**: `prom/prometheus:v2.20.1`
     - **Volumes**:
       - Binds `prometheus.yml` from the current directory to `/etc/prometheus/prometheus.yml` inside the container.
       - Uses the `prometheus_data` volume for persistent data storage.
     - **Ports**: Forwards port `9090` on the host to port `9090` in the container.
     - **Exposed Port**: Makes port `9090` accessible to other containers.
     - **Network**: Connects the container to the `my-network` network.
   
   4. **Start Grafana Container**
   - Starts a Grafana container with the following configurations:
     - **Name**: `grafana`
     - **Image**: `grafana/grafana:7.1.5`
     - **Volumes**:
       - Binds `datasources.yml` from the current directory to `/etc/grafana/provisioning/datasources/datasources.yml` inside the container.
       - Uses the `grafana_data` volume for persistent data storage.
     - **Environment Variables**:
       - Configures Grafana settings for authentication.
     - **Ports**: Forwards port `3001` on the host to port `3000` in the container.
     - **Exposed Port**: Makes port `3000` accessible to other containers.
     - **Network**: Connects the container to the `my-network` network.
   
   5. **Build Node.js Application Image**
   - Builds a Docker image named `myapp` for a Node.js application using the `docker_image` module. It uses the Dockerfile located in the `./codebase_partner` directory.
   
   6. **Start Node.js Application Container**
   - Starts a container for the Node.js application using the `myapp` image previously built:
     - **Name**: `myapp`
     - **Image**: `myapp`
     - **Ports**: Forwards port `3000` on the host to port `3000` in the container.
     - **Exposed Port**: Makes port `3000` accessible to other containers.
     - **Network**: Connects the container to the `my-network` network.
   
   Please ensure that the necessary files (`prometheus.yml`, `datasources.yml`, and `Dockerfile`) exist in the correct locations and contain the required configurations for this setup to work properly. Also, ensure Docker is installed and running on the target machine where this playbook is executed.

  </details>

### 5. Run the Ansible playbook "ansible-deploy-containers.yml" file.

```
ansible-playbook ansible-deploy-containers.yml 
```


<img src="https://github.com/otam-mato/nodejs_ansible/assets/113034133/9918631b-85c5-44cb-8bac-e91eb8d685cc" width="700px"/>


