# Restaurant_tips_analysis
## I. Introduction

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/restaurant_tips.png)

This project aims to use the restaurant tips dataset to practice creating composition plots and visualizations. We will examine the relationship between different variables and the tips given.

The dataset consists of information from 244 restaurant bills, collected in the US in 1987.

It includes details about the tips given to restaurant staff, such as the total bill, tip amount, gender of the person paying, smoking status, day of the week, time of day, and party size.

## II. Data Source:
- Name: Restaurant Tips Analysis
- Source: csv hosted on GitHub "https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv"

## III. Data exploration
- **Do people who smoke give more tips?**
Let's figure out the difference between smokers and non-smokers in terms of their behavior and purchasing habits in public catering establishments.
```
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read.csv('https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv')
smokers_df = df.query('smoker == "Yes"')
smokers_df.head()
```
|index|id|total\_bill|tip|sex|smoker|day|time|size|
|---|---|---|---|---|---|---|---|---|
|56|56|38\.01|3\.0|Male|Yes|Sat|Dinner|4|
|58|58|11\.24|1\.76|Male|Yes|Sat|Dinner|2|
|60|60|20\.29|3\.21|Male|Yes|Sat|Dinner|2|
|61|61|13\.81|2\.0|Male|Yes|Sat|Dinner|2|
|62|62|11\.02|1\.98|Male|Yes|Sat|Dinner|2|
```
non_smokers_df = df.query('smoker == "No"')
non_smokers_df.head()
```
|index|id|total\_bill|tip|sex|smoker|day|time|size|
|---|---|---|---|---|---|---|---|---|
|0|0|16\.99|1\.01|Female|No|Sun|Dinner|2|
|1|1|10\.34|1\.66|Male|No|Sun|Dinner|3|
|2|2|21\.01|3\.5|Male|No|Sun|Dinner|3|
|3|3|23\.68|3\.31|Male|No|Sun|Dinner|2|
|4|4|24\.59|3\.61|Female|No|Sun|Dinner|4|

- **How do smoker and non-smoker group tip?**
```
# With the whole dataset 
common_tip_min = df['tip'].min()
common_tip_max = df['tip'].max()
common_tip_mean = df['tip'].mean()
common_tip_median = df['tip'].median()

# Make a list of values
common_values = [common_tip_min, common_tip_max, common_tip_mean, common_tip_median]
# Round all the values to 4 decimal places
common_values = map(lambda x: round(x, 4), common_values)

# Make a dataframe from the list
common_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])
# Output the dataframe
common_mct
```
|index|0|
|---|---|
|min|1\.0|
|max|10\.0|
|mean|2\.9983|
|median|2\.9|
```
# With Smokers group
smokers_tip_min = smokers_df['tip'].min()
smokers_tip_max = smokers_df['tip'].max()
smokers_tip_mean = smokers_df['tip'].mean()
smokers_tip_median = smokers_df['tip'].median()

# Make a list of values
common_values = [smokers_tip_min, smokers_tip_max, smokers_tip_mean, smokers_tip_median]
# Round all the values to 4 decimal places
common_values = map(lambda x: round(x,4), common_values)

#Make a dataframe from the list
smokers_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])
# Output the dataframe
smokers_mct
```
|index|0|
|---|---|
|min|1\.0|
|max|10\.0|
|mean|3\.0087|
|median|3\.0|

```
# With Non-smokers group
non_smokers_tip_min = non_smokers_df['tip'].min()
non_smokers_tip_max = non_smokers_df['tip'].max()
non_smokers_tip_mean = non_smokers_df['tip'].mean()
non_smokers_tip_median = non_smokers_df['tip'].median()

common_values = [non_smokers_tip_min, non_smokers_tip_max, non_smokers_tip_mean, non_smokers_tip_median]
common_values = map(lambda x: round(x,4), common_values)

#Make a dataframe from the list
non_smokers_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])
# Output the dataframe
non_smokers_mct
```
|index|0|
|---|---|
|min|1\.0|
|max|9\.0|
|mean|2\.9919|
|median|2\.74|

- **Compare their measures of central tendency.**
Let's show the retrieved results together
```
all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Smokers': {'min': smokers_tip_min, 'max': smokers_tip_max, 'mean': smokers_tip_mean, 'median': smokers_tip_median},
    'Non-smokers': {'min': non_smokers_tip_min, 'max': non_smokers_tip_max, 'mean': non_smokers_tip_mean, 'median': non_smokers_tip_median}
}

# Make a dataframe
all_mct = pd.DataFrame(all_vals_dict)
# Output the dataframe
all_mct
```
|index|Common|Smokers|Non-smokers|
|---|---|---|---|
|min|1\.0|1\.0|1\.0|
|max|10\.0|10\.0|9\.0|
|mean|2\.99827868852459|3\.008709677419355|2\.9918543046357615|
|median|2\.9|3\.0|2\.74|


- **Insights based on measures of central tendency comparison.**

- **Whole dataset tips histogram**
```
plt.figure(figsize=(15,5))
plt.hist(df['tip'], bins=5, color='#74b9ff')
plt.xlabel('Tip value')
plt.ylabel('Frequency')
plt.title('Whole dataset tip values')
plt.grid(True)
plt.show()
```

![whole dataset tip values](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/whole%20dataset%20tip%20values.png)

- **Smokers tips histogram**
```
plt.figure(figsize=(15,5))
plt.hist(smokers_df['tip'], bins=5, color='#ff7675')
plt.xlabel('Tip value')
plt.ylabel('Frequency')
plt.title('Smokers tip values')
plt.grid(True)
plt.show()
```

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/smokers%20tips%20hist.png)

- **Non-smokers tips histogram**
```
plt.figure(figsize=(15,5))
plt.hist(smokers_df['tip'], bins=5, color='#55efc4')
plt.xlabel('Tip value')
plt.ylabel('Frequency')
plt.title('Non-smokers tip values')
plt.grid(True)
plt.show()
```

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/non-smokers%20tips%20hist.png)

- **Extra-task with a higher difficulty**
```
figure, axis = plt.subplots(1,3, figsize=(15,5))
axis[0].hist(df['tip'], bins=5, color="#74b9ff")
axis[0].set_title("Whole dataset tip values")

axis[1].hist(smokers_df['tip'], bins=5, color="#74b9ff")
axis[1].set_title("Smokers tip values")

axis[2].hist(non_smokers_df['tip'], bins=5, color="#74b9ff")
axis[2].set_title("Non-smokers tip values")
```

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/total%20hist.png)

## Conclusion
- **General conclusion:**
    - Khách hút thuốc (smokers) và không hút thuốc (non-smokers) đều có phân bố tiền tip tương đối giống nhau, tuy nhiên:

        - Trung bình, khách hút thuốc có xu hướng để tiền tip thấp hơn một chút so với nhóm không hút thuốc.

        - Nhóm không hút thuốc thường có phạm vi tip rộng hơn và xuất hiện nhiều giá trị tip cao hơn.

        - Nhìn chung, việc hút thuốc không ảnh hưởng quá lớn đến số tiền tip, nhưng khách không hút thuốc có vẻ hào phóng hơn đôi chút.

- **Do males give more tips?**
```
plt.figure(figsize=(12,4))
plt.subplot(1,3,1)
plt.hist(df['tip'], bins=10, color='skyblue')
plt.title('Whole dataset tip values')

plt.subplot(1,3,2)
plt.hist(df[df['sex'] == 'Male']['tip'], bins=10, color='skyblue')
plt.title('Male tip values')

plt.subplot(1,3,3)
plt.hist(df[df['sex'] == 'Female']['tip'], bins=10, color='skyblue')
plt.title('Female tip values')
plt.show()
```

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/male-female%20tips.png)

**Insight 1:**
- Nam giới thường cho tip cao hơn trung bình so với nữ giới.

- Phân bố tip của nam có nhiều giá trị cao hơn, chứng tỏ họ có xu hướng tip hào phóng hơn.

- Tuy vậy, phần lớn tip nhỏ ở cả hai giới đều tập trung quanh mức trung bình, cho thấy không có sự chênh lệch quá lớn.

- **Do weekends bring more tips?**
```
plt.figure(figsize=(12,4))
plt.subplot(1,3,1)
plt.hist(df['tip'], bins=10, color='skyblue')
plt.title('Whole dataset tip values')

plt.subplot(1,3,2)
plt.hist(df[df['day'].isin(['Sat', 'Sun'])]['tip'], bins=10, color='skyblue')
plt.title('Weekend tip values')

plt.subplot(1,3,3)
plt.hist(df[~df['day'].isin(['Sat', 'Sun'])]['tip'], bins=10, color='skyblue')
plt.title('Weekday tip values')
plt.show()
```

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/weekend-weekday%20tips.png)

**Insight 2:** 
- Cuối tuần (Saturday, Sunday) có xu hướng nhận được tiền tip cao hơn so với các ngày trong tuần.

- Lý do có thể là vào cuối tuần, mọi người đi ăn thư giãn, chi tiêu thoải mái hơn.

- Ngày trong tuần tip thấp hơn một chút, có thể do các bữa ăn nhanh, ít mang tính giải trí.

- **Do dinners bring more tips?**
```
plt.figure(figsize=(12,4))
plt.subplot(1,3,1)
plt.hist(df['tip'], bins=10, color='skyblue')
plt.title('Whole dataset tip values')

plt.subplot(1,3,2)
plt.hist(df[df['time'] == 'Dinner']['tip'], bins=10, color='skyblue')
plt.title('Dinner tip values')

plt.subplot(1,3,3)
plt.hist(df[df['time'] == 'Lunch']['tip'], bins=10, color='skyblue')
plt.title('Lunch tip values')
plt.show()
```

![](https://github.com/dulcie130435/Restaurant_tips_analysis/raw/main/dinner-lunch%20tips.png)

**Insight 3:**
- Bữa tối (Dinner) có mức tip trung bình cao hơn đáng kể so với bữa trưa (Lunch).

- Bữa tối thường là bữa chính trong ngày, có thể đi kèm đồ uống hoặc tiệc nhỏ, dẫn đến hóa đơn cao hơn → tip cao hơn.

- Bữa trưa thường mang tính nhanh gọn, nên tip thấp hơn.
