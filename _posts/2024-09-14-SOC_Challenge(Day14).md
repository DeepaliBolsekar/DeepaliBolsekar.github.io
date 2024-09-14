---
title: "Day-14 Alerts and Dashboards in Kibana"
date: 2024-09-14
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day14of30]
---


![kibana-cover](/assets/alert-dashboard-1/kibana.png){: width="500" height="300" }

**Let's Create Alerts and Dashboards for Ubuntu Server Authentication Logs**

Today, we'll dive into creating alerts and dashboards in Kibana to visualize our Ubuntu server's authentication logs.

- Log in to your cloud provider and access your Vultr or preferred cloud service account.
- Connect to Elasticsearch using your login credentials to connect to your Elasticsearch instance.
- Navigate to Kibana for that click on the hamburger icon and select "Discover" under "Analytics" to begin creating alerts and dashboards.

![discover.png](/assets/alert-dashboard-1/discover.png){: width="500" height="300" }

- Let's dive into setting up an alert!  Over on the **left-hand pane**, you'll find a list of available fields.  Look for the `agent.name` field.
- Clicking on that field will reveal the two agents we created throughout the challenge.  Since we're interested in creating an alert for the Linux agent, let's add it as a filter.  Just click the **plus icon** to include it.

![agent.name-linux.png](/assets/alert-dashboard-1/agent.name-linux.png){: width="500" height="300" }

- **Let's focus on system authentication events:**

- Next, we'll look for the field named `system.ssh.auth.event`. Click on this field to view the different types of system authentication events. We're primarily interested in **failed** events. Let's add this filter to our query.

![failed-auth-field.png](/assets/alert-dashboard-1/failed-auth-field.png){: width="500" height="300" }

- Next field: Source IP. Knowing the source IP addresses of most SSH authentication attempts can help you identify and address potential security threats. Add this field to your table by clicking the plus icon.

![source-ip-field.png](/assets/alert-dashboard-1/source-ip-field.png){: width="500" height="300" }

- We'll also add a column for the **source country field**. This will help us pinpoint the geographic origin of each log entry, providing valuable insights into potential threats and attack patterns.

![country-field.png](/assets/alert-dashboard-1/country-field.png){: width="500" height="300" }

- Now, let's focus on the next field: **username**. This will help us identify which usernames are being targeted in the SSH brute force attacks.

![username-field.png](/assets/alert-dashboard-1/username-field.png){: width="500" height="300" }

- These are all the selected fields.

![selected-fields.png](/assets/alert-dashboard-1/selected-fields.png){: width="500" height="300" }

- And here's what the results will look like after applying all the necessary filters and columns.

![required-fields-dash.png](/assets/alert-dashboard-1/required-fields-dash.png){: width="500" height="300" }

- Now, save your search by giving it an appropriate name.

![save-search.png](/assets/alert-dashboard-1/save-search.png){: width="500" height="300" }

- Now, to create an alert, click on "Alerts" in the top right corner. Select the first option, "Create search threshold rule”.

![create-alert.png](/assets/alert-dashboard-1/create-alert.png){: width="500" height="300" }

- Provide an appropriate name for your alert, and you'll see the Elasticsearch query selected automatically.

![rule-name-elastic-query.png](/assets/alert-dashboard-1/rule-name-elastic-query.png){: width="500" height="300" }

- In the "Define Your Query" section, you'll discover a comprehensive list of filters and conditions we've thoughtfully configured for our alerts. Feel free to customize these condition settings to match your specific needs.

![define-query-details.png](/assets/alert-dashboard-1/define-query-details.png){: width="500" height="300" }

- To test the query, I'll adjust the query time to 5 days, click the 'Test Query' button, and examine the results. As expected, the query is displaying 4 events that occurred within the last 5 days. After testing you can revert the changes.

![test-query-result.png](/assets/alert-dashboard-1/test-query-result.png){: width="500" height="300" }

- Moving forward, we'll see that the system will check for alert conditions every minute. You can customize this interval to suit your specific needs. Once you've finished configuring the alert, click the **Save** button to apply your changes.

![save-rule.png](/assets/alert-dashboard-1/save-rule.png){: width="500" height="300" }

- To create the map, let's copy the filter query we've created.

![write-KQL-for-map.png](/assets/alert-dashboard-1/write-KQL-for-map.png){: width="500" height="300" }

- Now, let's create a dashboard. From the Analytics menu, click on Maps.

![map.png](/assets/alert-dashboard-1/map.png){: width="500" height="300" }

- Paste your query into the search bar and then click the "Add Layer" button.

![add-layer.png](/assets/alert-dashboard-1/add-layer.png){: width="500" height="300" }

- Let's use a Choropleth map. This type of map will shade geographical areas based on specific alert conditions.

![choropleth.png](/assets/alert-dashboard-1/choropleth.png){: width="500" height="300" }

- For source boundaries, we'll select Administrative Boundaries and EMS boundries set to "World Countries." This will help us identify brute force attack attempts from around the globe. Once you choose EMS boundaries, the join field will be automatically populated.

![world-countries.png](/assets/alert-dashboard-1/world-countries.png){: width="500" height="300" }

- Below is the data view from the Discover page. We'll use this same view for our map.

![data-view-1.png](/assets/alert-dashboard-1/data-view-1.png){: width="500" height="300" }

- For the join field, select the "source geo country iso code." Then, add and continue to create the map.

![dataview-2.png](/assets/alert-dashboard-1/dataview-2.png){: width="500" height="300" }

- You can customize your dashboard map further using the following options:

![layer-settings-no-change.png](/assets/alert-dashboard-1/layer-settings-no-change.png){: width="500" height="300" }

- Now, click "Save" in the upper right corner, give your map a name, and select "New" to add it to a new dashboard. Then, save your changes.

![new-dashboard.png](/assets/alert-dashboard-1/new-dashboard.png){: width="500" height="300" }

- After clicking "Save and Go to Dashboard," you'll be redirected to the dashboard. There, you'll find your map displayed prominently.

![dashboard-1.png](/assets/alert-dashboard-1/dashboard-1.png){: width="500" height="300" }

- Let's create another map similar to this one, but focusing on successful attempts. To do this, duplicate the existing map by clicking on the three dots in the top right corner and selecting "Duplicate."
- From there, you can modify the map's name and query as “Accepted” from “Failed” to reflect your desired changes. Once you've made the necessary adjustments, apply them to see the updated map.

![apply-success-name.png](/assets/alert-dashboard-1/apply-success-name.png){: width="500" height="300" }

![query-sucess-map.png](/assets/alert-dashboard-1/query-sucess-map.png){: width="500" height="300" }

- Now, **save the dashboard** with a descriptive name and description.

![save-dashboard.png](/assets/alert-dashboard-1/save-dashboard.png){: width="500" height="300" }

- "Behold, the final masterpiece of my dashboard! Isn't it a sight to behold?” 😍

![done.png](/assets/alert-dashboard-1/done.png){: width="500" height="300" }

**Great work! 🎉** We now have a powerful alert system in place that will trigger every 5 minutes for specific queries based on predefined conditions. This, combined with our user-friendly dashboard, provides a real-time view of any suspicious activity, such as attacks or brute force attempts, on our Ubuntu server.