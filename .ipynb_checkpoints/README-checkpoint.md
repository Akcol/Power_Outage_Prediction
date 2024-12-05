# Power_Outage_Prediction

By Alex Collier

<body>
<section id="dataset-introduction">
  <h3>Introduction to the Dataset and Prediction Question</h3>
  <p>
    The dataset we are using focuses on <strong>major power outages</strong> across various regions. 
    It contains detailed records of outages, including the causes, durations, affected populations, 
    and geographic information. This dataset offers insights into the factors that contribute to 
    power outages and the severity of their impacts.
  </p>
  <p>
    Our central question is: <em>"What causes most major power outages, and can we predict the most likely cause of an outage?"</em>
  </p>
  <p>
    Understanding the root causes of power outages and predicting them is crucial for improving power grid 
    reliability, preparing for natural disasters, and reducing the socioeconomic impacts of outages. Power outages 
    can disrupt daily life, damage economies, and threaten public safety. Utilities, policymakers, and researchers 
    can leverage insights from this analysis to better allocate resources, design preventative measures, and 
    strengthen infrastructure.
  </p>
</section>
<section id="data-description">
  <h3>Dataset Variables and Descriptions</h3>
    <p>The original DataFrame contains 1534 rows, corresponding to 1534 outages, and 57 columns. Listed below are just some of the columns provided to us.</p>
  <table>
    <thead>
      <tr>
        <th>Column Name</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>YEAR</td>
        <td>Year when the outage occurred.</td>
      </tr>
      <tr>
        <td>MONTH</td>
        <td>Month when the outage occurred.</td>
      </tr>
      <tr>
        <td>U.S._STATE</td>
        <td>Full name of the state where the outage occurred.</td>
      </tr>
      <tr>
        <td>POSTAL.CODE</td>
        <td>Two-letter postal abbreviation for the state.</td>
      </tr>
      <tr>
        <td>CLIMATE.REGION</td>
        <td>Climate region associated with the location of the outage.</td>
      </tr>
      <tr>
        <td>ANOMALY.LEVEL</td>
        <td>Severity level of climate anomalies during the outage.</td>
      </tr>
      <tr>
        <td>OUTAGE.START.DATE</td>
        <td>Date when the outage began.</td>
      </tr>
      <tr>
        <td>OUTAGE.RESTORATION.DATE</td>
        <td>Date when the outage was restored.</td>
      </tr>
      <tr>
        <td>CAUSE.CATEGORY</td>
        <td>General category of the cause of the outage (e.g., severe weather).</td>
      </tr>
      <tr>
        <td>OUTAGE.DURATION</td>
        <td>Total duration of the outage in minutes.</td>
      </tr>
      <tr>
        <td>DEMAND.LOSS.MW</td>
        <td>Total megawatt loss in demand during the outage.</td>
      </tr>
      <tr>
        <td>CUSTOMERS.AFFECTED</td>
        <td>Total number of customers affected by the outage.</td>
      </tr>
      <tr>
        <td>RES.PRICE</td>
        <td>Residential electricity price in cents per kilowatt-hour.</td>
      </tr>
      <tr>
        <td>POPULATION</td>
        <td>Population of the affected region.</td>
      </tr>
      <tr>
        <td>POPDEN_URBAN</td>
        <td>Population density in urban areas (persons per square mile).</td>
      </tr>
      <tr>
        <td>POPDEN_RURAL</td>
        <td>Population density in rural areas (persons per square mile).</td>
      </tr>
    </tbody>
  </table>
</section>

<section id="data-cleaning">
    <h2>Data Cleaning and Preprocessing</h2>
    <p>The following steps were undertaken to clean and preprocess the dataset, ensuring its readiness for analysis and modeling:</p>
    <ol>
        <li>
            <strong>Handling Missing Values</strong>
            <ul>
                <li><strong>Action Taken:</strong> Missing values in critical columns such as <code>CAUSE.CATEGORY</code>, <code>OUTAGE.DURATION</code>, and <code>CUSTOMERS.AFFECTED</code> were either filled with appropriate imputed values (like median for numeric columns) or removed if imputation wasn't feasible.</li>
                <li><strong>Reasoning:</strong> Missing values could bias analyses, especially when predicting causes or durations of outages. Imputation or removal ensured the integrity of the dataset for training machine learning models.</li>
                <li><strong>Effect on Analysis:</strong> Reduced the dataset size slightly, but ensured clean input for models and accurate results.</li>
            </ul>
        </li>
        <li>
            <strong>Correcting Data Types</strong>
            <ul>
                <li><strong>Action Taken:</strong> Converted columns like <code>OUTAGE.START.DATE</code> and <code>OUTAGE.START.TIME</code> into a single datetime column (<code>OUTAGE.START</code>). Similarly, <code>OUTAGE.RESTORATION</code> was created as a combined column.</li>
                <li><strong>Reasoning:</strong> Ensured that timestamps could be used effectively in duration calculations and time-based analyses.</li>
                <li><strong>Effect on Analysis:</strong> Enabled easy calculations of <code>OUTAGE.DURATION</code> by subtracting <code>OUTAGE.START</code> from <code>OUTAGE.RESTORATION</code>.</li>
            </ul>
        </li>
        <iframe src="https://Akcol.github.io/Power_Outage_Prediction/Images/head_output.html" width="100%" height="300px" frameborder="0"></iframe>
    </ol>
</section>

<section id="data-exploration">
   <h2>Data Exploration</h2> 
    <h3>Univariate: Outages by Cause Category</h3>
<p>
    This bar chart displays the distribution of power outages by their cause categories. I wanted to see the distribution of major cuases of power outages.
</p>
<iframe src="https://Akcol.github.io/Power_Outage_Prediction/Images/outage_by_cat.html" width="100%" height="500px" frameborder="0"></iframe>
    <h3>Bivariate: Outage Duration by Cause Category</h3>
    <p>
 The plot below shows the relation between outage duration and cause category. It shows that outages with the longest duration tend to be from a fuel supply emergency.
</p>
    <iframe src="https://Akcol.github.io/Power_Outage_Prediction/Images/outage_dur_cat.html" width="100%" height="500px" frameborder="0"></iframe>
    <h3>Interesting Aggregates: Average Outage Duration by Climate Region and Cause Category</h3>
    <p>
    This heatmap displays the average outage duration across various climate regions and cause categories. It highlights that outages caused by severe weather in the
    East North Central region tend to last significantly longer, emphasizing the need for targeted infrastructure resilience strategies in that area.
    </p>
<iframe src="https://Akcol.github.io/Power_Outage_Prediction/Images/avg_out_dur_CR_CC.html" width="100%" height="300px" frameborder="0"></iframe>
</section>

<section id="Prediction">
    <h3>Prediction Problem and Type</h3>
<p>This is a <strong>regression problem</strong>, as the goal is to predict the <strong>duration of a power outage</strong> (a continuous variable) based on various characteristics of the region, the cause of the outage, and population-specific metrics.</p>

<h3>Response Variable</h3>
<p>The response variable is <code>OUTAGE.DURATION</code>, which measures the length of a power outage in minutes. This variable was chosen because understanding and predicting outage duration is crucial for resource allocation, planning restoration efforts, and minimizing disruption caused by power outages.</p>

<h3>Metric for Evaluation</h3>
<p>The primary evaluation metric is <strong>Mean Absolute Error (MAE)</strong>, as it provides an interpretable measure of the average error in minutes, which is directly relevant to stakeholders. MAE was chosen over other metrics (e.g., RMSE) because it is less sensitive to large errors and better captures the typical error magnitude.</p>

<h3>Features Used for Prediction</h3>
<p>Features included in the model are <code>CAUSE.CATEGORY</code>, <code>CLIMATE.REGION</code>, <code>NERC.REGION</code>, <code>POPULATION</code>, and other region- or cause-specific metrics such as <code>POPDEN_URBAN</code> and <code>POPDEN_RURAL</code>. These features are selected because they are available at the time of prediction and provide critical context about the outage's circumstances. Features like restoration times are excluded as they would not be known before the outage occurs.</p>

<h3>Hypothesis</h3>
<p>The hypothesis is that the duration of a power outage can be accurately predicted using information about the region's climate, population metrics, and the cause of the outage. For instance, outages caused by severe weather in densely populated areas might have longer durations due to infrastructure challenges and resource constraints.</p>
</section>

<section id="baseline">
    <h3>Baseline Model</h3>

<p>
My model is a multiclass classifier using the features <strong>CLIMATE.REGION</strong> and <strong>OUTAGE.DURATION</strong> to predict the cause of a major outage. This information is essential for energy companies and policymakers to better understand the underlying causes of outages and allocate resources effectively to mitigate future disruptions.
</p>

<p><strong>The features are:</strong></p>
<ul>
    <li><strong>CLIMATE.REGION</strong> (nominal): Represents the geographic climate region of the outage, which can influence the type of weather or environmental factors leading to outages.</li>
    <li><strong>OUTAGE.DURATION</strong> (quantitative): Measures the length of the outage in hours, providing insight into the severity of the event and potentially the type of cause.</li>
</ul>

<p>
The target variable was <strong>CAUSE.CATEGORY</strong>, which includes categories such as "severe weather," "intentional attack," and others. These were left as-is to allow the model to handle multiclass classification.
</p>

<p>
The performance of this model was moderate, with an overall accuracy of <strong>65%</strong> on the test set. The model performed well for large categories like <strong>Severe Weather</strong> and <strong>Intentional Attack</strong> but struggled with less frequent causes such as <strong>Equipment Failure</strong> and <strong>Fuel Supply Emergency</strong>. While this provides a good starting point, improvements are needed to handle class imbalances and better predict underrepresented categories.
</p>

</section>

</body>