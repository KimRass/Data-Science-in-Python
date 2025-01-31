# Setting
## Display Hangul
```python
path = "C:/Windows/Fonts/malgun.ttf"
if platform.system() == "Darwin":
    mpl.rc("font", family="AppleGothic")
elif platform.system() == "Windows":
    font_name = mpl.font_manager.FontProperties(fname=path).get_name()
    mpl.rc('font', family=font_name)
```
- `family`: (`"NanumBarunGothic"`)
## Display Minus Sign
```python
mpl.rc("axes", unicode_minus=False)
```
## Plot Style
```python
plt.style.use("dark_background")
```
- (`"default"`, `"dark_background"`)

# Charts
## Common Arguments
- `lw`
- `label`
- `fontsize`
- `title`
- `legend`: (bool)
- `xlim`, `ylim`
- `figsize`
- `grid`
- `marker`
	- `"o"`: Circle
	- `"*"`: Star
	- `"."`: Point
	- `"+"`: Plus
- `linestyle` (= `ls`)
	- `"-"`: Solid line
	- `"--"`: Dashed line
	- `"-."`: Dash-dot line
	- `":"`: Dotted line
- `color` (= `c`)
	- `"b"`: Blue
	- `"g"`: Green
	- `"r"`: Red
	- `"c"`: Cyan
	- `"m"`: Magenta
	- `"y"`: Yellow
	- `"k"` black
	- `"w"`: White
## Line Chart
- Reference: https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html
### `plt.plot()`
### `DataFrame.plot.line([style=[...], [ax])`, `Series.plot.line([ax])`
- `style`: For example, `["k--", "bo-", "r*"]`
- `figsize`
## Pie Chart
```python
# `x`: The fractional area of each wedge is given by `x / sum(x)`
# `startangle`
# Example
wedges, text = ax.pie(
	x=values,
	labels=labels,
	labeldistance=1.05,
	colors=codes,
	textprops={"fontsize": 100, "color": "black"},
	wedgeprops={"edgecolor": "black", "linewidth": 5},
	startangle=90,
	radius=1,
	counterclock=False,
	explode=explode
)
```
### `sns.lineplot(x, y, [linewidth], [color], [label])`
## Scatter Plot
```python
# Reference: https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html
# `s`
# `cmap`: (`"RdYlBu"`, ...)
# `alpha`
# `edgecolors`
# `linewidths`: The linewidth of the marker edges
# `marker`
plt.scatter([s], [c], [cmap], [alpha], [edgecolors], [linewidth])
<df>.plot.scatter(y, x, c, grid, figsize, cmap, [ax])
```
### `sns.scatterplot(ax, data, x, y, hue, hue_norm, palette, s, alpha)`
## Bar Chart
```python
plt.bar(x, height)

# Reference: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.plot.barh.html
# `x`: If not specified, the index of the DataFrame is used.
# `y`: If not specified, all numerical columns are used.
DataFrame.plot.barh(x, y, [stacked], [color])
Series.plot.barh()

plt.barh(y, width, height, [alpha], [color], [label], [edgecolor], [linewidth])

sns.barplot(ax, x, y, color, edgecolor, orient)
```
## Histogram
### `ax.hist()`, `DataFrame.plot.hist([ax])`, `Series.plot.hist([ax])`
```python
ax.hist(cnt_genre["genre"], bins=30)
```
```python
raw_data.hist(bins=20, grid=True, figsize=(16,12))
```
## Box Plot
### `ax.boxplot()`, `DataFrame.boxplot(column, by, grid, figsize)`, `Series.boxplot()`
## Horizontal Line & Vertical Line
```python
# [color], [ls], [lw], [label]
plt.axvline(x=0, ymin=0, ymax=1)
ax.axvline()
```
### `hlines()`, `vlines()`
## `ax.text()`
```python
# `va`
# `ha`: (`"left"`, `"center"`, `"right"`)
ax.text(x, y, s, va, ha, fontsize, [color], [stretch])
```
## Span
```python
# `alpha`, `color`
plt.axvspan(xmin, xmax, ymin=0, ymax=1)
```
## Fill Area
```python
# Example
plt.fill_between()
```
## Heat Map
- Seaborn implementation
	- Reference: http://seaborn.pydata.org/generated/seaborn.heatmap.html
	```python
	# `center`: The value at which to center the colormap when plotting divergant data. Using this parameter will change the default `cmap` if none is specified.
	# `mask`: If passed, data will not be shown in cells where `mask` is True. Cells with missing values are automatically masked.
	sns.heatmap([ax], data, [annot=True], [annot_kws={"size"}], [fmt=".2f"], [linewidths], [linecolor], [center], [cmap], [cbar=True], [mask])
	```
- Matplotlib implementation
	```python
	plt.pcolormesh([cmap])
	plt.colorbar()
	```
## `sns.countplot(ax, [data], [x], [y], [hue], [orient])`
- Reference: https://seaborn.pydata.org/generated/seaborn.countplot.html
- Show the counts of observations in each categorical bin using bars.
- [`data`]: (DataFrame)
- [`orient`]: (`"v"`, `"h"`)
```python
sns.countplot(ax=axes, data=train_df, x="Pclass", hue="Survived")
```
## ETC
### `sns.lmplot(data, x, y, fit_reg, line_kws, size, aspect, ci, sharey)`
- `data`: (DataFrame)
- `fit_reg`: (bool) If `True`, estimate and plot a regression model relating the x and y variables.
- `ci`: (int in [0, 100] or None, optional) Size of the confidence interval for the regression estimate. This will be drawn using translucent bands around the regression line. The confidence interval is estimated using a bootstrap for large datasets, it may be advisable to avoid that computation by setting this parameter to None.
- `aspect`: Aspect ratio of each facet, so that aspect\*height gives the width of each facet in inches.
<!-- ### `sns.distplot(a, norm_hist)`
- `a`: (Series, 1d-Array, or List)
- `norm_hist`: (bool, optional) If `True`, the histogram height shows a density rather than a count. This is implied if a KDE or fitted density is plotted. -->
### `sns.replot(x, y, col, hue, style, kind, data)`
### `sns.kedplot(ax, data)`
### `sns.stripplot(x, y, data, jitter, edgecolor, size)`
### `sns.pairtplot()`

# Grid
#### `ax.grid()`
```python
plt.grid()

ax.grid(axis="x", color="White", alpha=0.3, linestyle="--", linewidth=2)
```

# Size
## Set figure size
```python
plt.figure(figsize=(w, h))
```
```python
fig.set_size_inches(w, h)
```

# Axis
## Axis off
```python
ax.axis("off")
```
## Set Axis Invisible
```python
ax.xaxis.set_visible(False)
```
## Set Axis Range
```python
plt.xlim([xmin, xmax])
ax.set_xlim([xmin, xmax])
ax.axis([xmin, xmax, ymin, ymax])
```
## Invert Axis
```python
plt.gca().invert_xaxis()
ax.invert_xaxis()
```
## Set Label Position
```python
ax.xaxis.set_label_position("top")
```
## Set Axis Label
```python
plt.xlabel()
ax.set_xlabel()
```

# Tick
## `ax.tick_params(axis, [which], [labelsize], [labelcolor], [labelrotation], [grid_linewidth], [labelsize])`
- `axis`: (`"x"`, `"y"`)
## Set Tick
```python
# `ticks`, `labels`, [`rotation`]
plt.xticks()
# `ticks`, `labels`
ax.set_xticks()
# Example
plt.xticks(np.arange(0, 3, 0.2))
```
## Set Tick Position
```python
# (`"top"`, `"bottom"`, `"left"`, `"right"`)
ax.xaxis.set_ticks_position()
```
## Set Tick Format
```python
# Example
ax.xaxis.set_major_formatter(mpl.ticker.StrMethodFormatter("{x:,.0f}"))
```
## Rotate Tick Label
```python
plt.xticks(rotation)
ax.tick_params(axis, labelrotation)
ax.set_xticklabels(ax.get_xticks(), rotation)
```
## Major and Minor Ticks
```python
# Example
from matplotlib.ticker import MultipleLocator

ax.xaxis.set_major_locator(MultipleLocator(0.5))
ax.xaxis.set_major_formatter("{x:.1f}")
ax.tick_params(axis="x", which="major", length=10, width=2, labelrotation=90)

ax.xaxis.set_minor_locator(MultipleLocator(0.1))
ax.tick_params(axis="x", which="minor", length=7, width=1)
```

# Title
## Set title
```python
plt.title()
ax.set_title()
```
- `size`: (float)

# Legend
## Place a legend
```python
plt.plot(xs, ys, label=label)
plt.legend()
```
- `loc`: (`"best"`, `"center"`, `"upper left"`, `"upper right"`, `"lower left"`, `"lower right"`, `"upper center"`, `"lower center"`, `"center left"`, `"center right"`)
- `bbox_to_anchor`: Box that is used to position the legend in conjunction with `loc`. This argument allows arbitrary placement of the legend.
- `fancybox`: Whether round edges should be enabled.
- `shadow`: Whether to draw a shadow behind the legend.
- `ncol`: The number of columns that the legend has.
- `fontsize`

# Color Bar
```python
img = ...
fig.colorbar(heatmap, ax=...)
plt.colorbar(img, format="%+2.0f dB")
```
### Set Color Bar Label
```python
cbar = ...
cbar.set_label(label="전용면적(m²)", size=15)
```

# Save Figure
```python
# `bbox_inches="tight"`
plt.savefig()
fig.savefig()
```

# Clear Figure
```python
from IPython.display import clear_output

...
clear_output()
```
```python
...
plt.close()
```

# Subplots
## `plt.subplot()`
```python
for i in range(9):
	ax = plt.subplot(3, 3, i + 1)
```
## `plt.subplots()`
```python
fig, axes = plt.subplots(nrows, ncols, ...)
```
- `figsize`
- `sharex`, `sharey`: (bool) Controls sharing of properties among x (`sharex`) or y (`sharey`) axes.

# Options
## `plt.setp()`
## `plt.show()`
## `plt.gcf().tight_layout()`, `fig.tight_layout()`
## `plt.imshow([cmap])`
## `plt.set()`
```python
# `title`
# `xlabel`, `ylabel`
# `xlim`, `ylim`
# `xticks`, `yticks`
ax.set(title="Example", xlabel="xAxis", ylabel="yAxis", xlim=[0, 1], ylim=[-0.5, 2.5], xticks=data.index, yticks=[1, 1.05, 1.1, 1.15, 1.2, 1.25, 1.3])
```
## `sns.set()`
- `palette`: (`"muted"`)
- `color_codes`: If `True` and `palette` is a seaborn palette, remap the shorthand color codes (e.g. `"b"`, `"g"`, `"r"`, etc.) to the colors from this palette.
- `font_scale`: (float)

# `networkx`
```python
improt networks as nx
```
## `nx.Graph()`
```python
g = nx.Graph()
```
## `nx.DiGraph()`
## `nx.circular_layout()`
```python
pos = nx.circular_layout(g)
```
## `nx.draw_networks_nodex()`
```python
nx.draw_networkx_nodes(g, pos, node_size=2000)
```
## `nx.draw_networkx_edges()`
```python
nx.draw_networkx_edges(g, pos, width=weights)
```
## `nx.draw_networkx_labels()`
```python
nx.draw_networkx_labels(g, pos, font_family=font_name, font_size=11)
```
## `nx.draw_shell()`
```python
nx.draw_shell(g, with_labels=False)
```
### `g.add_nodes_from()`
```python
g.add_nodes_from(set(df.index.get_level_values(0)))
```
### `g.add_edge()`
```python
for _, row in df.iterrows():
    g.add_edge(row.name[0], row.name[1], weight=row["cowork"]/200)
```
### `g.edges()`
```python
weights = [cnt["weight"] for (_, _, cnt) in g.edges(data=True)]
```

# `mapboxgl`
## `mapboxgl.viz`
```python
from mapboxgl.viz import *
```
### `CircleViz()`
```python
viz = CircleViz(data=geo_data, access_token=token, center=[127.46,36.65], zoom=11, radius=2, stroke_color="black", stroke_width=0.5)
```
### `GraduatedCircleViz()`
```python
viz = GraduatedCircleViz(data=geo_data, access_token=token, height="600px", width="600px", center=(127.45, 36.62), zoom=11, scale=True, legend_gradient=True, add_snapshot_links=True, radius_default=4, color_default="black", stroke_color="black", stroke_width=1, opacity=0.7)
```
### `viz.style`
```python
viz.style = "mapbox://styles/mapbox/outdoors-v11"
```
- (`"mapbox://styles/mapbox/streets-v11"`, `"mapbox://styles/mapbox/outdoors-v11"`, `"mapbox://styles/mapbox/light-v10"`
- `"mapbox://styles/mapbox/dark-v10"`, `"mapbox://styles/mapbox/satellite-v9"`, `"mapbox://styles/mapbox/satellite-streets-v11"`, `"mapbox://styles/mapbox/navigation-preview-day-v4"`, `"mapbox://styles/mapbox/navigation-preview-night-v4"`, `"mapbox://styles/mapbox/navigation-guidance-day-v4"`, `"mapbox://styles/mapbox/navigation-guidance-night-v4"`)
### `viz.show()`
### `viz.create_html()`
```python
with open("D:/☆디지털혁신팀/☆실거래가 분석/☆그래프/1km_store.html", "w") as f:
    f.write(viz.create_html())
```
## `mapboxgl.utils`
```python
from mapboxgl.utils import df_to_geojson, create_color_stops, create_radius_stops
```
### `DataFrame.to_geojson()`
```python
geo_data = df_to_geojson(df=df, lat="lat", lon="lon")
```
### `viz.create_color_stops()`
```python
viz.color_property = "error"
viz.color_stops = create_color_stops([0, 10, 20, 30, 40, 50], colors="RdYlBu")
```
### `viz.create_radius_stops()`
```python
viz.radius_property = "errorl"
viz.radius_stops = create_radius_stops([0, 1, 2], 4, 7)
```