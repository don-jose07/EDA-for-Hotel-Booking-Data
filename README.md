# Hotel Booking Demand Analysis

## Project Overview
This project presents an end-to-end Exploratory Data Analysis (EDA) on a hotel booking dataset. The primary goal is to understand booking patterns, customer behavior, and factors influencing hotel demand and cancellations. The analysis includes data cleaning, univariate and bivariate analysis, group-wise analysis, time-series analysis, and derivation of actionable business insights and recommendations.

## Dataset
The dataset, `hotel_booking_dataset.csv`, contains various features related to hotel bookings, including:
- Booking details (e.g., `Booking_ID`, `Booking_Date`, `Arrival_Date`, `Lead_Time_Days`)
- Guest information (e.g., `Adults`, `Children`, `Babies`, `Customer_Type`, `Country`)
- Hotel specifics (e.g., `Hotel_Type`, `Hotel_Location`, `Room_Type_Reserved`, `Room_Type_Assigned`)
- Financial metrics (e.g., `ADR` (Average Daily Rate), `Estimated_Revenue`)
- Reservation status and changes (e.g., `Reservation_Status`, `Is_Canceled`, `Booking_Changes`, `Deposit_Type`)
- Satisfaction scores and special requests.

## Exploratory Data Analysis (EDA) Steps

### 1. Data Understanding and Quality Assessment
- **Initial Overview**: Loaded the dataset and examined its structure, data types, and summary statistics using `df.head()`, `df.info()`, and `df.describe(include='all')`.
- **Duplicate Records**: Identified and removed 180 duplicate rows and 180 duplicate `Booking_ID` entries, reducing the dataset size to 25,000 records.
- **Data Type Correction**: Converted `Booking_Date`, `Arrival_Date`, and `Reservation_Status_Date` columns to `datetime64[ns]`.
- **Missing Value Handling**:
    - Dropped `Company_ID` due to ~82% missing values.
    - Imputed missing `Children` values with 0.
    - Imputed missing `Agent_ID`, `ADR`, and `Satisfaction_Score` with their respective medians.
    - Imputed missing `Hotel_Location`, `Country`, and `Meal_Type` with their respective modes.
    - Converted `Children` and `Agent_ID` to integer types.
- **Inconsistent Values (Categorical Data)**:
    - Standardized entries in `Hotel_Type` (e.g., 'CITY HOTEL' to 'City Hotel'), `Market_Segment` (e.g., 'Online TA ' to 'Online TA'), and `Meal_Type` (e.g., 'bb' to 'BB').
    - Created a new binary feature `Is_Room_Type_Changed` (1 if `Room_Type_Reserved` != `Room_Type_Assigned`, else 0).
- **Outlier Detection**: Identified potential outliers in numerical columns using box plots and the IQR method. Outliers were noted but not removed, as their treatment depends on specific modeling goals.

### 2. Univariate Analysis
- **Descriptive Statistics**: Summarized central tendency, dispersion, and shape of numerical feature distributions.
- **Distribution of Numerical Features**: Visualized distributions using histograms to understand skewness and kurtosis.
- **Frequency Distribution for Categorical Features**: Plotted count plots to show the frequency of each category.

### 3. Bivariate Analysis
- **Correlation Matrix**: Generated a heatmap to visualize correlations between numerical features.
- **Numerical vs. Categorical Features**: Explored relationships such as `Estimated_Revenue` by `Hotel_Type`, `ADR` by `Market_Segment`, and `Lead_Time_Days` by `Reservation_Status`.
- **Categorical vs. Categorical Features**: Analyzed relationships like `Reservation_Status` by `Hotel_Type`, `Cancellation` by `Deposit_Type`, and `Cancellation` by `Customer_Type`.

### 4. Group-wise Analysis
- Segmented data by `Hotel_Type` and `Customer_Type` to compare average estimated revenue, ADR, and total bookings across groups.

### 5. Time-Series Analysis (Monthly Trends)
- Extracted `Arrival_Month` and `Arrival_Year`.
- Visualized monthly trends in total bookings and average ADR to identify seasonal patterns.

## Key Business Insights

1.  **High Occupancy in City Hotels, Higher ADR in Resort Hotels**: City Hotels handle more bookings, while Resort Hotels consistently achieve higher average daily rates and estimated revenue per booking, suggesting different market positioning and pricing strategies.

2.  **Significant Seasonality**: Both total bookings and ADR show clear seasonal patterns, peaking in summer months and around year-end. This highlights opportunities for dynamic pricing and resource planning.

3.  **Lead Time and Deposit Type Impact Cancellations**: Bookings with 'Non Refund' deposits exhibit lower cancellation rates, emphasizing the effectiveness of stricter policies in securing reservations.

4.  **Customer Type Influences Behavior**: Different customer segments display distinct booking patterns (lead times, stay durations, cancellation likelihood), indicating a need for tailored marketing and loyalty programs.

5.  **Room Type Discrepancies**: Instances where assigned room types differed from reserved ones were identified, pointing to potential areas for improving customer satisfaction and operational efficiency.

## Practical Recommendations

1.  **Dynamic Pricing Strategy**: Implement dynamic pricing models to adjust rates according to seasonal demand, increasing rates during peak seasons and offering promotions during off-peak periods.

2.  **Optimize Marketing and Resource Allocation**: Tailor marketing campaigns for City (volume) vs. Resort (premium) hotels. Allocate resources efficiently to manage high traffic in City Hotels and cater to higher-value guests in Resort Hotels.

3.  **Strategic Deposit Policies**: Encourage 'Non Refund' deposit types, especially for long lead-time or peak-season bookings, to minimize cancellations. Clearly communicate policy benefits.

4.  **Tailored Customer Engagement**: Develop personalized loyalty programs and offers for different customer segments (e.g., corporate rates for 'Contract' customers, direct booking incentives for 'Transient' guests).

5.  **Investigate Room Type Discrepancies**: Analyze the root causes and impact of `Is_Room_Type_Changed` on customer satisfaction to streamline room assignment processes and enhance guest experience.

6.  **Analyze Lead Time vs. Cancellation Trade-offs**: Further research the relationship between lead time, booking channels, and cancellation rates to optimize booking window strategies.

7.  **Leverage Guest Satisfaction Scores**: Continuously monitor and analyze `Satisfaction_Score` to identify key drivers of positive experiences and improve services.

## Tools and Libraries Used
-   **Python**
-   **Pandas** for data manipulation and analysis.
-   **NumPy** for numerical operations.
-   **Matplotlib** for static visualizations.
-   **Seaborn** for enhanced statistical data visualization.

## How to Replicate
1.  Clone this repository.
2.  Ensure you have the required Python libraries installed (`pandas`, `numpy`, `matplotlib`, `seaborn`).
3.  Place `hotel_booking_dataset.csv` in the project root directory.
4.  Run the Jupyter Notebook (or Google Colab notebook) cells sequentially to reproduce the analysis.
