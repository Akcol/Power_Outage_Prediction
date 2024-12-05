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
            <iframe src="/Images/head_output.html" width="100%" height="300px" frameborder="0"></iframe>
    </ol>
</section>
</body>