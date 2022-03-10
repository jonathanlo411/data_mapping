# Data Mapping

This notebook was created to map CAIDA Users and ASes by country. Current size is a world map.

## Running Notebook
The notebook using [Geopandas](https://geopandas.org/en/stable/) and [Geoplot](https://residentmario.github.io/geoplot/). This means that you will need to set up a virtual environment. Personally, I used [this](https://medium.com/analytics-vidhya/fastest-way-to-install-geopandas-in-jupyter-notebook-on-windows-8f734e11fa2b) Medium article by [Tanish Gupta](https://tanish-gupta.medium.com/) to set up my environment. 

To run the notebook:
1. Activate conda virtual env that has Geopandas by running the following command in Anaconda Prompt
 ```
 conda activate yourenv
```
2. Launch notebook menu using:
```
jupyter notebook
```
3. Navigate to notebook and run


## Details
When using the Geopandas package, the documentation does not discuss multivariate maps. However, you can use base maps then plot on top of them. In the below example, a choropleth map is plotted first in `ax`. Then, a point plot is plotted on top of the `ax`.

~~~Python
scheme_one = mc.FisherJenks(merged['num_users'], k=7)

ax = gplt.choropleth(
    merged,
    hue='num_users',
    scheme=scheme_one,
    cmap='Blues',
    legend=True,
    figsize=(18,14)
)
gplt.pointplot(
    merged_centroids,
    ax=ax,
    scale='num_ASes',
    color='red',
    legend=True,
    limits=(3, 30),
    legend_values=[400, 200, 100, 50, 25, 10],
    legend_labels=['≤ 400 ASes', '≤ 200 ASes', '≤ 100 ASes', '≤ 50 ASes', '≤ 25 ASes', '≤ 10 ASes']
)
~~~

Since, Geopandas is built on top of Matplotlib, you can utilize underlying  Matplotlib functions for legends an plots.

~~~Python
plt.title("ASes and Users by Country")
ax.get_legend().set_title("Users")
plt.savefig('ases_and_users_by_country.png')
~~~

The code will return: ![](https://cdn.discordapp.com/attachments/942218891952783421/951328638517800990/ases_and_users_by_country.png)
