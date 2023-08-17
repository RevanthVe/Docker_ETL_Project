# Fetch_ETL_Project

Application Deployment and Assumptions

1. Deployment in Production:
   - Use containerization (e.g., Docker) to package the application and its dependencies.
   - Deploy these containers on orchestration platforms like Kubernetes or AWS ECS for easy scaling and management.

2. Making it Production Ready:
   - Add logging for debugging and monitoring purposes.
   - Implement error-handling mechanisms to gracefully manage failures.
   - Include automated tests to ensure code reliability.
   - Implement security measures such as database encryption and secure connections.

3. Scaling with Growing Dataset:
   - Implement a message processing queue to handle high volumes of incoming messages.
   - Use auto-scaling groups or Kubernetes' autoscaling for the application.
   - Use database replicas to distribute read loads.

4. Recovering PII Data:
   - The current setup uses irreversible hashing for PII, so direct recovery isn't possible.
   - For PII recovery, use encryption (which is reversible) instead of hashing.
   - Securely store the decryption keys.

5. Assumptions Made:
   - All messages in the SQS have a consistent structure.
   - The local setup (localstack and Postgres) mirrors the production environment.
   - MD5 hashing is sufficient for masking PII, and the hashed values won't collide.

Step by step guide to run the code:
- Install Python, Git, Docker and Docker-Compose.
- On terminal, Clone the repository by using command: git clone repo_url
- Open the repository using command: cd Fetch_ETL_Project
- Start the Localstack and Postgres Containers using Docker-Compose command: docker-compose up -d
- Install Necessary Python Libraries: pip install boto3 psycopg2
- Run Python code: python work_code.py
- Verify Data insertion: psql -d postgres -U postgres -p 5432 -h localhost -W
- After connecting, to query data, use: SELECT * FROM user_logins;

## Next Steps

Apart from the points mentioned above,
- **Logging:** Implement a robust logging system to monitor the operations of the application, which will aid in troubleshooting and ensuring data integrity.
- **Optimization:** As the dataset grows, we'll need to optimize the data fetching process from SQS. Considering paginated fetching or stream processing might be beneficial.
- **Unit Tests:** Incorporate unit tests to ensure each component of the application works as expected and to catch any potential bugs early in the development phase.





