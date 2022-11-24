# snyk_api_dashboard
Automating vulnerability monitoring with Snyk, Prometheus and Grafana

#### Reference
Snyk Blog on Snyk_Exporter

https://snyk.io/blog/vulnerability-monitoring-with-snyk-prometheus-and-grafana/

The YouTube between the Lunar team, who developed the Snyk_Exporter, and Snyk

https://www.youtube.com/watch?v=zJsxAx7MKKk

## Preparation

Get the files of the project, and set environment variables below
1. SNYK_TOKEN - set Snyk Group level API TOKEN, either of service account or a PAT
2. SNYK_ORG_1 - set Snyk Org ID of one org
3. SNYK_ORG_2 - set Snyk Org ID of other org

Three environment variables above would be reflected in `app/docker-compose.yml`, lines 17 to 19.
* More Snyk Org's may be added to include projects from more Snyk Org's displayed in the dashboard.
<img width="418" alt="Screenshot 2022-11-22 at 22 02 08" src="https://user-images.githubusercontent.com/93645043/203320622-894857b3-3760-4298-90d1-70a02447fa28.png">

## Test run the snyk_exporter x grafana x prometheus dashboard
1. start `DockerDesktop`, and wait for DockerDesktop to get started
2. From the directory, `app`, run the command, `docker-compose up -d`
3. Use a web browser to access URLs below:

   3.1. Grafana    - http://localhost:3000/
        
        3.1.1. Default UserId/Password : `admin/admin`
        
   3.2. Prometheus - http://localhost:9090/targets?search=
        
        3.2.1. Confirm both targets of prometheus is OK in status
        <img width="1206" alt="Screenshot 2022-11-22 at 22 17 55" src="https://user-images.githubusercontent.com/93645043/203323681-60dbeef0-cac4-40f6-857a-7bce1df584dd.png">
4. Wait a few minutes for `snyk_exporter` to scrape issues of projects imported into Snyk, using Snyk API
   
   Run the command, `curl http://localhost:9532/metrics`
   
   4.1. Response of the CURL without Snyk API response on issues
   <img width="670" alt="Screenshot 2022-11-22 at 22 22 20" src="https://user-images.githubusercontent.com/93645043/203324807-271e4241-56ef-43cc-9b9e-913a030e68be.png">
   
   4.2. Reponse of the CURL with Snyk API response on issues
   <img width="944" alt="Screenshot 2022-11-22 at 22 22 50" src="https://user-images.githubusercontent.com/93645043/203324934-408ad268-d09f-40e0-a7f2-aa0565cfcc86.png">
5. Access Grafana dashboard after you see issues of projects from Snyk API in response of CURL
<img width="1427" alt="Screenshot 2022-11-22 at 22 25 50" src="https://user-images.githubusercontent.com/93645043/203325372-19c90246-d8c6-4d0e-a42e-02a7eec20675.png">

6. To stop the POC dashboard, enter the command, `docker-compose down -v`

* Reminder: Grafana dashboard is in read-only mode.  Grafana config files would need to be adjusted to create/adjust the dashboard.
