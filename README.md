# Data Engineering: Building an Automated Data Pipeline

# Automated Data Pipeline for Gans' E-Scooter Sharing System

## Overview
**Gans**, a startup focused on sustainable mobility, aims to provide an e-scooter-sharing system in the world's most populous cities. Competing with established players, Gans prioritizes operational efficiency by ensuring scooters are positioned where users need them most. This inspired the creation of an **automated data pipeline** to predict e-scooter movements.

## Phase 1: Building the Local Pipeline

### Challenges and Decisions
1. **Local vs. Online Environment**  
   - **Advantages of Local Development**:
     - Full control and easier debugging.
     - Maximized use of local resources without cloud limitations.
     - Rapid iteration and experimentation for a solid foundation.

2. **Data Collection**  
   - **APIs**: Gathered structured data from various sources with parameters like country and population.  
     Example: For Germany, retrieved cities with a minimum population of 500,000.  
   - **Tables Created**:  
     - **cities_info**: General city data including location and population.  
     - **airports**: Nearby airports within a 50km radius fetched using the Aerodatabox API, ensuring optimal scooter positioning.  
     - **flights**: Automated fetching of next-day flight data, capturing arrivals in comprehensive time windows.  
     - **weather_info**: Weather forecasts retrieved using the OpenWeatherMap API, aiding location-based decisions.

   - **Why Use `pd.json_normalize()`?**  
     Flattened nested JSON from APIs into a tabular format for easier manipulation, enhancing data usability.

3. **Data Transformation**  
   - Key transformations included adjusting column positions, removing duplicates, aligning data types, and renaming columns for consistency.  

4. **Data Storage**  
   - Built and maintained local SQL databases, addressing the importance of converting API "time" strings into MySQL-compatible `DATETIME` types.

## Phase 2: Migrating to the Cloud

### Transitioning to Google Cloud Platform (GCP)
1. **Cloud SQL**  
   Configured a scalable MySQL instance on GCP, seamlessly integrating with data scripts.


![image](https://github.com/user-attachments/assets/2dc65873-3d66-47cf-9952-fa07e0f122a6)


3. **Cloud Functions**  
   - Migrated scripts to GCP using `functions_framework.http` with minor adjustments:
     - Added HTTP request handling for external triggers.
     - Used environment variables to manage sensitive data securely.
     - Resolved deployment issues, including missing dependencies and Error 500, by reviewing logs and configurations.


4. **Cloud Scheduler**  
   Automated pipeline execution to ensure consistent and reliable data processing.

### Common Challenges in Cloud Deployment
- Connection configuration and permissions.
- Dependency management via `requirements.txt`.
- Debugging deployment errors through detailed logs in GCP.

## Conclusion
From local pipelines to cloud-based solutions, this project established a scalable, automated system to predict e-scooter movements for Gans. The journey showcased the importance of starting locally to build a strong foundation and then transitioning to the cloud for enhanced scalability and automation. Overcoming challenges like compatibility and dependency management, the project is set to transform urban mobility.

[Read more about this project on Medium](https://medium.com/@sina.khodadadi.ds/data-engineering-building-an-automated-data-pipeline-aec969f1a5c9)
