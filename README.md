python
#Import numpy for calculations and matplolib for charting
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import random
```


```python
# Import our data into pandas from CSV
clinical_trial = 'clinicaltrial_data.csv'
clinical_trial_df = pd.read_csv(clinical_trial)
clinical_trial_df

mouse_drug = 'mouse_drug_data.csv'
mouse_drug_df = pd.read_csv(mouse_drug)
mouse_drug_df

combined_df = pd.merge(clinical_trial_df, mouse_drug_df, on = "Mouse ID")
combined_df.head()


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b128</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b128</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b128</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b128</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
</div>



# Tumor Response to Treatments


```python
# tumor_volume_mean = combined_df.groupby(["Drug", "Timepoint"]).mean()["Tumor Volume (mm3)"]
# tumor_volume_mean = pd.DataFrame(tumor_volume_mean)
# tumor_volume_mean
```


```python
# tumor_volume_sem = combined_df.groupby(["Drug", "Timepoint"]).sem()["Tumor Volume (mm3)"]
# tumor_volume_sem = pd.DataFrame(tumor_volume_sem)
# tumor_volume_sem.head()
```


```python
Tumor_response_df = combined_df[["Drug", "Timepoint","Tumor Volume (mm3)"]]
Tumor_response_df = Tumor_response_df.groupby(["Drug", "Timepoint"])["Tumor Volume (mm3)"].mean()
Tumor_response_df = pd.DataFrame(Tumor_response_df)
Tumor_response_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Tumor Volume (mm3)</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">Capomulin</th>
      <th>0</th>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44.266086</td>
    </tr>
    <tr>
      <th>10</th>
      <td>43.084291</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42.064317</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.716325</td>
    </tr>
    <tr>
      <th>25</th>
      <td>39.939528</td>
    </tr>
    <tr>
      <th>30</th>
      <td>38.769339</td>
    </tr>
    <tr>
      <th>35</th>
      <td>37.816839</td>
    </tr>
    <tr>
      <th>40</th>
      <td>36.958001</td>
    </tr>
    <tr>
      <th>45</th>
      <td>36.236114</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Ceftamin</th>
      <th>0</th>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>46.503051</td>
    </tr>
    <tr>
      <th>10</th>
      <td>48.285125</td>
    </tr>
    <tr>
      <th>15</th>
      <td>50.094055</td>
    </tr>
    <tr>
      <th>20</th>
      <td>52.157049</td>
    </tr>
    <tr>
      <th>25</th>
      <td>54.287674</td>
    </tr>
    <tr>
      <th>30</th>
      <td>56.769517</td>
    </tr>
    <tr>
      <th>35</th>
      <td>58.827548</td>
    </tr>
    <tr>
      <th>40</th>
      <td>61.467895</td>
    </tr>
    <tr>
      <th>45</th>
      <td>64.132421</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Infubinol</th>
      <th>0</th>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47.062001</td>
    </tr>
    <tr>
      <th>10</th>
      <td>49.403909</td>
    </tr>
    <tr>
      <th>15</th>
      <td>51.296397</td>
    </tr>
    <tr>
      <th>20</th>
      <td>53.197691</td>
    </tr>
    <tr>
      <th>25</th>
      <td>55.715252</td>
    </tr>
    <tr>
      <th>30</th>
      <td>58.299397</td>
    </tr>
    <tr>
      <th>35</th>
      <td>60.742461</td>
    </tr>
    <tr>
      <th>40</th>
      <td>63.162824</td>
    </tr>
    <tr>
      <th>45</th>
      <td>65.755562</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Ramicane</th>
      <th>0</th>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>43.944859</td>
    </tr>
    <tr>
      <th>10</th>
      <td>42.531957</td>
    </tr>
    <tr>
      <th>15</th>
      <td>41.495061</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.238325</td>
    </tr>
    <tr>
      <th>25</th>
      <td>38.974300</td>
    </tr>
    <tr>
      <th>30</th>
      <td>38.703137</td>
    </tr>
    <tr>
      <th>35</th>
      <td>37.451996</td>
    </tr>
    <tr>
      <th>40</th>
      <td>36.574081</td>
    </tr>
    <tr>
      <th>45</th>
      <td>34.955595</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Stelasyn</th>
      <th>0</th>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47.527452</td>
    </tr>
    <tr>
      <th>10</th>
      <td>49.463844</td>
    </tr>
    <tr>
      <th>15</th>
      <td>51.529409</td>
    </tr>
    <tr>
      <th>20</th>
      <td>54.067395</td>
    </tr>
    <tr>
      <th>25</th>
      <td>56.166123</td>
    </tr>
    <tr>
      <th>30</th>
      <td>59.826738</td>
    </tr>
    <tr>
      <th>35</th>
      <td>62.440699</td>
    </tr>
    <tr>
      <th>40</th>
      <td>65.356386</td>
    </tr>
    <tr>
      <th>45</th>
      <td>68.438310</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Zoniferol</th>
      <th>0</th>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>46.851818</td>
    </tr>
    <tr>
      <th>10</th>
      <td>48.689881</td>
    </tr>
    <tr>
      <th>15</th>
      <td>50.779059</td>
    </tr>
    <tr>
      <th>20</th>
      <td>53.170334</td>
    </tr>
    <tr>
      <th>25</th>
      <td>55.432935</td>
    </tr>
    <tr>
      <th>30</th>
      <td>57.713531</td>
    </tr>
    <tr>
      <th>35</th>
      <td>60.089372</td>
    </tr>
    <tr>
      <th>40</th>
      <td>62.916692</td>
    </tr>
    <tr>
      <th>45</th>
      <td>65.960888</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 1 columns</p>
</div>




```python
Tumor_response_df["Volume SEM"] = Tumor_response_df["Tumor Volume (mm3)"].sem()

Tumor_response_df = pd.DataFrame(Tumor_response_df)
Tumor_response_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Tumor Volume (mm3)</th>
      <th>Volume SEM</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44.266086</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>10</th>
      <td>43.084291</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42.064317</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.716325</td>
      <td>0.898067</td>
    </tr>
  </tbody>
</table>
</div>




```python
tumor_response_pivot = Tumor_response_df.pivot_table(index = "Timepoint", columns = "Drug", values = "Tumor Volume (mm3)")
tumor_response_pivot.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44.266086</td>
      <td>46.503051</td>
      <td>47.062001</td>
      <td>47.389175</td>
      <td>46.796098</td>
      <td>47.125589</td>
      <td>47.248967</td>
      <td>43.944859</td>
      <td>47.527452</td>
      <td>46.851818</td>
    </tr>
    <tr>
      <th>10</th>
      <td>43.084291</td>
      <td>48.285125</td>
      <td>49.403909</td>
      <td>49.582269</td>
      <td>48.694210</td>
      <td>49.423329</td>
      <td>49.101541</td>
      <td>42.531957</td>
      <td>49.463844</td>
      <td>48.689881</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42.064317</td>
      <td>50.094055</td>
      <td>51.296397</td>
      <td>52.399974</td>
      <td>50.933018</td>
      <td>51.359742</td>
      <td>51.067318</td>
      <td>41.495061</td>
      <td>51.529409</td>
      <td>50.779059</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.716325</td>
      <td>52.157049</td>
      <td>53.197691</td>
      <td>54.920935</td>
      <td>53.644087</td>
      <td>54.364417</td>
      <td>53.346737</td>
      <td>40.238325</td>
      <td>54.067395</td>
      <td>53.170334</td>
    </tr>
  </tbody>
</table>
</div>




```python
tumor_response_pivot_sem = Tumor_response_df.pivot_table(index = "Timepoint", columns = "Drug", values = "Volume SEM")
tumor_response_pivot_sem.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
      <td>0.898067</td>
    </tr>
  </tbody>
</table>
</div>




```python
# tumor_volume.plot[kind = "scatter", x = "Time (Days)", y = "Tumor Valume (mm3)", title = "Tumor Response to Treatmanet"]
# plt.show
```


```python
plt.errorbar(tumor_response_pivot.index, tumor_response_pivot["Capomulin"], yerr=tumor_response_pivot_sem["Capomulin"], color ="r", marker = "o", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(tumor_response_pivot.index, tumor_response_pivot["Infubinol"], yerr=tumor_response_pivot_sem["Infubinol"], color ="b", marker = "+", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(tumor_response_pivot.index, tumor_response_pivot["Ketapril"], yerr=tumor_response_pivot_sem["Ketapril"], color ="g", marker = "*", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(tumor_response_pivot.index, tumor_response_pivot["Placebo"], yerr=tumor_response_pivot_sem["Placebo"], color ="y", marker = "^", markersize=5, linestyle="--", linewidth=0.5)

x_lim = len(tumor_response_pivot.index)
plt.title("Tumor Response to Treatment")
plt.xlabel("Time (Days)")
plt.ylabel("Tumor Volume (mm3)")
plt.show()
```


![png](output_10_0.png)


# Metastatic Response to Treatment



```python
metastatic_response_df = combined_df[["Drug", "Timepoint","Metastatic Sites"]]
metastatic_response_df = metastatic_response_df.groupby(["Drug", "Timepoint"])["Metastatic Sites"].mean()
metastatic_response_df = pd.DataFrame(metastatic_response_df)
metastatic_response_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Metastatic Sites</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.160000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.320000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.652174</td>
    </tr>
  </tbody>
</table>
</div>




```python
metastatic_response_df["Volume SEM"] = metastatic_response_df["Metastatic Sites"].sem()
metastatic_response_df = pd.DataFrame(metastatic_response_df)
metastatic_response_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Metastatic Sites</th>
      <th>Volume SEM</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>0.000000</td>
      <td>0.090044</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.160000</td>
      <td>0.090044</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.320000</td>
      <td>0.090044</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.375000</td>
      <td>0.090044</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.652174</td>
      <td>0.090044</td>
    </tr>
  </tbody>
</table>
</div>




```python
metastatic_response_pivot = metastatic_response_df.pivot_table(index = "Timepoint", columns = "Drug", values = "Metastatic Sites")
metastatic_response_pivot.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.160000</td>
      <td>0.380952</td>
      <td>0.280000</td>
      <td>0.304348</td>
      <td>0.260870</td>
      <td>0.375000</td>
      <td>0.320000</td>
      <td>0.120000</td>
      <td>0.240000</td>
      <td>0.166667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.320000</td>
      <td>0.600000</td>
      <td>0.666667</td>
      <td>0.590909</td>
      <td>0.523810</td>
      <td>0.833333</td>
      <td>0.565217</td>
      <td>0.250000</td>
      <td>0.478261</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.375000</td>
      <td>0.789474</td>
      <td>0.904762</td>
      <td>0.842105</td>
      <td>0.857143</td>
      <td>1.250000</td>
      <td>0.764706</td>
      <td>0.333333</td>
      <td>0.782609</td>
      <td>0.809524</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.652174</td>
      <td>1.111111</td>
      <td>1.050000</td>
      <td>1.210526</td>
      <td>1.150000</td>
      <td>1.526316</td>
      <td>1.000000</td>
      <td>0.347826</td>
      <td>0.952381</td>
      <td>1.294118</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.errorbar(metastatic_response_pivot.index, metastatic_response_pivot["Capomulin"], yerr=tumor_response_pivot_sem["Capomulin"], color ="r", marker = "o", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(metastatic_response_pivot.index, metastatic_response_pivot["Infubinol"], yerr=tumor_response_pivot_sem["Infubinol"], color ="b", marker = "+", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(metastatic_response_pivot.index, metastatic_response_pivot["Ketapril"], yerr=tumor_response_pivot_sem["Ketapril"], color ="g", marker = "*", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(metastatic_response_pivot.index, metastatic_response_pivot["Placebo"], yerr=tumor_response_pivot_sem["Placebo"], color ="y", marker = "^", markersize=5, linestyle="--", linewidth=0.5)

x_lim = len(tumor_response_pivot.index)
plt.title("Metastatic Response to Treatment")
plt.xlabel("Time (Days)")
plt.ylabel("Metastatic Sites")
plt.show()
```


![png](output_15_0.png)


# Survival Rates


```python
survival_rates_df = combined_df[["Drug", "Timepoint","Mouse ID"]]
survival_rates_df = survival_rates_df.groupby(["Drug", "Timepoint"])["Mouse ID"].count()
survival_rates_df = pd.DataFrame(survival_rates_df)
survival_rates_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Mouse ID</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>25</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>25</td>
    </tr>
    <tr>
      <th>15</th>
      <td>24</td>
    </tr>
    <tr>
      <th>20</th>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
#survival_rates_df["Volume SEM"] = survival_rates_df["Mouse ID"].sem()
#survival_rates_df = pd.DataFrame(survival_rates_df)
#survival_rates_df.head()

```


```python
survival_rates_df["Volume SEM"] = survival_rates_df["Mouse ID"].sem()
survival_rates_df = pd.DataFrame(survival_rates_df)
survival_rates_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Mouse ID</th>
      <th>Volume SEM</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>25</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>10</th>
      <td>25</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>15</th>
      <td>24</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>20</th>
      <td>23</td>
      <td>0.478596</td>
    </tr>
  </tbody>
</table>
</div>




```python
survival_rates_pivot = survival_rates_df.pivot_table(index = "Timepoint", columns = "Drug", values = "Mouse ID")
survival_rates_pivot
survival_rates_pivot_sem = survival_rates_df.pivot_table(index = "Timepoint", columns = "Drug", values = "Volume SEM")
survival_rates_pivot_sem.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
      <td>0.478596</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.errorbar(survival_rates_pivot.index, survival_rates_pivot["Capomulin"], yerr=tumor_response_pivot_sem["Capomulin"], color ="r", marker = "o", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(survival_rates_pivot.index, survival_rates_pivot["Infubinol"], yerr=tumor_response_pivot_sem["Infubinol"], color ="b", marker = "+", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(survival_rates_pivot.index, survival_rates_pivot["Ketapril"], yerr=tumor_response_pivot_sem["Ketapril"], color ="g", marker = "*", markersize=5, linestyle="--", linewidth=0.5)
plt.errorbar(survival_rates_pivot.index, survival_rates_pivot["Placebo"], yerr=survival_rates_pivot_sem["Placebo"], color ="y", marker = "^", markersize=5, linestyle="--", linewidth=0.5)

x_lim = len(tumor_response_pivot.index)
plt.title("Survival Rates to Treatment")
plt.xlabel("Time (Days)")
plt.ylabel("Mouse ID")
plt.show()
```


![png](output_21_0.png)


# Summary Bar Graph


```python
#Calculate the percentage change in tumor volume for each drug
tumor_volume_change_percentage =  ((tumor_response_pivot.iloc[-1]-tumor_response_pivot.iloc[0])/tumor_response_pivot.iloc[0]) * 100
tumor_volume_change_percentage
```




    Drug
    Capomulin   -19.475303
    Ceftamin     42.516492
    Infubinol    46.123472
    Ketapril     57.028795
    Naftisol     53.923347
    Placebo      51.297960
    Propriva     47.241175
    Ramicane    -22.320900
    Stelasyn     52.085134
    Zoniferol    46.579751
    dtype: float64




```python
tumor_volume_change_percentage.index
drug = list(tumor_volume_change_percentage.index)
drug
```




    ['Capomulin',
     'Ceftamin',
     'Infubinol',
     'Ketapril',
     'Naftisol',
     'Placebo',
     'Propriva',
     'Ramicane',
     'Stelasyn',
     'Zoniferol']




```python
tumor_percent_change = list(tumor_volume_change_percentage.values)
tumor_percent_change
```




    [-19.475302667894155,
     42.516491855897414,
     46.12347172785184,
     57.02879468660604,
     53.923347134769195,
     51.29796048315153,
     47.24117486320634,
     -22.32090046276666,
     52.085134287898995,
     46.57975086509522]




```python
colors = ['r' if tpc > 0 else 'g' for tpc in tumor_percent_change]
colors

```




    ['g', 'r', 'r', 'r', 'r', 'r', 'r', 'g', 'r', 'r']




```python
x_axis = np.arange(len(tumor_percent_change))
x_axis
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
#Bar chart
plt.bar(x_axis, tumor_percent_change, color = colors, align="edge")
tick_locations = [value for value in x_axis]
plt.xticks(tick_locations, tumor_volume_change_percentage.index)
plt.xlim(0, len(x_axis))
plt.ylim(-20, max(tumor_volume_change_percentage.values))
plt.title("Tumor Change Over 45 Day Treatment")
plt.xlabel("Drugs")
plt.ylabel("% Tumor Volume Change")
plt.savefig("% Tumor Volume Change")
plt.show()
```


![png](output_28_0.png)



```python
 Your objective is to analyze the data to show how four treatments 
compare.


Creating a scatter plot that shows how the tumor volume changes over time for each treatment.
Creating a scatter plot that shows how the number of metastatic (cancer spreading) sites changes over time for each treatment.
Creating a scatter plot that shows the number of mice still alive through the course of treatment (Survival Rate)
Creating a bar graph that compares the total % tumor volume change for each drug across the full 45 days.
As final considerations:

You must use the Pandas Library and the Jupyter Notebook.
You must use the Matplotlib and Seaborn libraries.
You must include a written description of three observable trends based on the data.
You must use proper labeling of your plots, including aspects like: Plot Titles, Axes Labels, Legend Labels, X and Y Axis Limits, etc.
Your scatter plots must include error bars. This will allow the company to account for variability between mice. You may want to look into pandas.DataFrame.sem for ideas on how to calculate this.
Remember when making your plots to consider aesthetics!
Your legends should not be overlaid on top of any data.
Your bar graph should indicate tumor redutumor growth as red and ction as green. It should also include a label with the percentage change for each bar. You may want to consult this tutorial for relevant code snippets.
You must include an exported markdown version of your Notebook called  README.md in your GitHub repository.
```


      File "<ipython-input-26-92a754469614>", line 1
        Your objective is to analyze the data to show how four treatments
                     ^
    SyntaxError: invalid syntax


