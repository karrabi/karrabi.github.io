The Write-Audit-Publish (WAP) pattern is a design pattern used in data engineering to ensure data quality and integrity within data pipelines. It involves three main stages:

1. **Write**:
   - Data is written to a non-production environment, such as a staging area or temporary storage. This ensures that the data is not immediately available to downstream consumers¹.

2. **Audit**:
   - The data is audited to check for quality issues and ensure it meets predefined data quality specifications. This step involves running data validation checks, such as verifying that there are no NULL values where they shouldn't be, and that fields are within expected ranges¹.

3. **Publish**:
   - Once the data passes the audit checks, it is published to the production environment where it becomes available to downstream consumers. This could involve merging the data from the staging area into the main table, or flipping a flag to include the data in user queries¹.

The WAP pattern helps maintain data integrity by ensuring that only validated data is made available to end-users and downstream processes. It is particularly useful in large-scale data operations where data quality is critical².
