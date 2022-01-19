# Setting
```python
fpath = "C:/Windows/Fonts/malgun.ttf"
font_name = mpl.font_manager.FontProperties(fname=fpath).get_name()
```
```python
mpl.rc("font", family=font_name)
```
- `family`: (`"NanumBarunGothic"`)
```python
mpl.rc("axes", unicode_minus=False)
```
```python
- (`"default"`, `"dark_background"`)
```

# Charts
## Common Arguments
- `ls`: (`"-"`, `"--"`, `"-."`, `":"`)
- `lw`
- `c`: Specifies a color.
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
- `linestyle`
	- `"-"`: Solid line
	- `"--"`: Dashed line
	- `"-."`: Dash-dot line
	- `":"`: Dotted line
- `color`
	- `"b"`: Blue
	- `"g"`: Green
	- `"r"`: Red
	- `"c"`: Cyan
	- `"m"`: Magenta
	- `"y"`: Yellow
	- `"k"` black
	- `"w"`: White
## Line Chart
### `plt.plot();`
```python
plot([arg1], arg2, [arg3], ...)
```python
plot("Column for x", "Column for y", data=pandas.DataFrame);
```
### `DataFrame.plot.line()`, `Series.plot.line()`
```python
data.plot.line(style=["k--", "bo-", "r*"], figsize=(20, 10));
```
- `style`
## Pie Chart
### `DataFrame.plot.pie()`, `Series.plot.pie()`
- `startangle`
## Scatter Plot
### `plt.scatter()`, `ax.scatter()`
```python
ax.scatter(gby["0.5km 내 교육기관 개수"], gby["실거래가"], s=70, c=gby["전용면적(m²)"], cmap="RdYlBu", alpha=0.7, edgecolors="black", linewidth=0.5)
```
### `DataFrame.plot.scatter()`
```python
data[data.workingday == 0].plot.scatter(y="count", x="hour", c="temp", grid=False, figsize=(12, 5), cmap="Blues")
```
- `s`
- `cmap`: ("RdYlBu")
- `alpha`
- `edgecolors`
## Bar Chart
### `ax.bar()`, `DataFrame.plot.bar()`, `Series.plot.bar()`
```python
ax.bar(x=nby_genre.index, height=nby_genre["movie_id"])
```
```python
data["label"].value_counts().plot.bar()
```
### `ax.barh()`, `DataFrame.plot.barh()`, `Series.plot.barh()`
```python
ax.barh(y=ipark["index"], width=ipark["가경4단지 84.8743A"], height=0.2, alpha=0.5, color="red", label="가경4단지 84.8743A", edgecolor="black", linewidth=1)
```
## Histogram
### `ax.hist()`, `DataFrame.plot.hist()`, `Series.plot.hist()`
```python
ax.hist(cnt_genre["genre"], bins=30)
```
```python
raw_data.hist(bins=20, grid=True, figsize=(16,12))
```
## Box Plot
### `ax.boxplot()`, `DataFrame.boxplot()`, `Series.boxplot()`
```python
raw_data.boxplot(column="count", by="season", grid=False, figsize=(12,5))
```
## Horizontal Line & Vertical Line
### `ax.axhline()`, `ax.axvline()`
```python
fig = ax.axhline(y=mean, color="r", ls=":", lw=2)
```
- `y`
### `hlines()`, `vlines()`
## `ax.text()`
```python
for _, row in ml_gby_ax.iterrows():
    ax.text(y=row["le"]-0.18, x=row["abs_error"], s=round(row["abs_error"], 1), va="center", ha="left", fontsize=10)
```
- `va`
- `ha`
- `fontsize`
- `s`
## `ax.fill_between()`
```python
ax.fill_between(x, y1, y2, ...)
```
## Heat Map
- Reference: http://seaborn.pydata.org/generated/seaborn.heatmap.html
```python
sb.heatmap([ax], data, [annot=True], [annot_kws={"size"}], [fmt=".2f"], [linewidths], [linecolor], [center], [cmap], [cbar=True], [mask])
```
- [`center`]: The value at which to center the colormap when plotting divergant data. Using this parameter will change the default `cmap` if none is specified.
- [`mask`]: If passed, data will not be shown in cells where `mask` is True. Cells with missing values are automatically masked.

# Grid
#### `ax.grid()`
```python
ax.grid(axis="x", color="White", alpha=0.3, linestyle="--", linewidth=2)
```

# Size
## Set figure size
```python
fig.set_size_inches(10, 10)
```

# Axis
## Axis off
```python
ax.axis("off")
```
## Set axis invisible
```python
ax.xaxis.set_visible(False)
# ax.yaxis.set_visible(False)
```
## `ax.axis()`
```python
ax.axis([2, 3, 4, 10])
```
## Set axis range
```python
ax.set_xlim([x1, x2])
# ax.set_ylim([y1, y2])
```
## `ax.xaxis.set_label_position()`, `ax.yaxis.set_label_position()`
```python
ax.xaxis.set_label_position("top")
```
## `ax.xaxis.set_ticks_position()`, `ax.yaxis.set_ticks_position()`
```python
ax.yaxis.set_ticks_position("right")
```
- (`"top"`, `"bottom"`, `"left"`, `"right"`)
## `ax.xaxis.set_major_formatter()`, `ax.yaxis.set_major_formatter()`
```python
ax.yaxis.set_major_formatter(mpl.ticker.StrMethodFormatter("{x:,.0f}"))
```
## `ax.invert_xaxis()`, `ax.invert_yaxis()`

# Tick
## `ax.set_xticks()`, `ax.set_yticks()`
## `ax.tick_params()`
```python
ax.tick_params(axis="x", labelsize=20, labelcolor="red", labelrotation=45, grid_linewidth=3)
```
## `ax.set_xticks()`, `ax.set_yticks()`
```python
ax.set_yticks(np.arange(1, 1.31, 0.05))
```
- 화면에 표시할 눈금을 설정합니다.

# Title
## Set title
```python
plt.title()
# ax.set_title()
```
- `size`: (float)

# Label
## `ax.set_xlabel()`, `ax.set_ylabel()`
```python
ax.set_xlabel("xAxis", size=15)
```

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
## `fig.colorbar()`
```python
cbar = fig.colorbar(ax=ax, mappable=scatter)
```
##### `cbar.set_label()`
```python
cbar.set_label(label="전용면적(m²)", size=15)
```

# Save
## `plt.savefig()`, `fig.savefig()`
```python
fig.savefig("means_plot_200803.png", bbox_inches="tight")
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
## `fig.tight_layout()`
## `ax.imshow()`
```python
ax.imshow(image.numpy().reshape(3,3), cmap="Greys")
```
## `ax.set()`
```python
ax.set(title="Example", xlabel="xAxis", ylabel="yAxis", xlim=[0, 1], ylim=[-0.5, 2.5], xticks=data.index, yticks=[1, 1.05, 1.1, 1.15, 1.2, 1.25, 1.3])
```
- `title`
- `xlabel`, `ylabel`
- `xlim`, `ylim`
- `xticks`, `yticks`
- Reference: https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D
# `seaborn`
```python
import seaborn as sb
```
### `sb.set()`
- `palette`: (`"muted"`)
- `color_codes`: If `True` and `palette` is a seaborn palette, remap the shorthand color codes (e.g. `"b"`, `"g"`, `"r"`, etc.) to the colors from this palette.
- `font_scale`: (float)
### `sb.lmplot()`
```python
sb.lmplot(data=resid_tr.iloc[1:], x="idx", y="resid", fit_reg=True, line_kws={"color": "red"}, size=5.2, aspect=2, ci=99, sharey=True)
```
- `data`: (DataFrame)
- `fit_reg`: (bool) If `True`, estimate and plot a regression model relating the x and y variables.
- `ci`: (int in [0, 100] or None, optional) Size of the confidence interval for the regression estimate. This will be drawn using translucent bands around the regression line. The confidence interval is estimated using a bootstrap; for large datasets, it may be advisable to avoid that computation by setting this parameter to None.
- `aspect`: Aspect ratio of each facet, so that aspect\*height gives the width of each facet in inches.
### `sb.distplot()`
```python
fig, axes = plt.subplots(1, 1, figsize=(7, 5))
fig = sb.distplot(ax=axes, a=resid_tr["resid"].iloc[1:], norm_hist=True, fit=stats.norm)
```
- `a`: (Series, 1d-Array, or List)
- `norm_hist`: (bool, optional) If `True`, the histogram height shows a density rather than a count. This is implied if a KDE or fitted density is plotted.
### `sb.scatterplot()`
```python
sb.scatterplot(ax=ax, data=df, x="ppa", y="error", hue="id", hue_norm=(20000, 20040), palette="RdYlGn", s=70, alpha=0.5)
```
### `sb.lineplot()`
```python
ax = sb.lineplot(x=data.index, y=data["ppa_ratio"], linewidth=3, color="red", label="흥덕구+서원구 아파트 평균")
```
### `sb.barplot()`
```python
sb.barplot(ax=ax, x=area_df["ft_cut"], y=area_df[0], color="brown", edgecolor="black", orient="v")
```
### `sb.countplot()`
```python
sb.countplot(ax=ax, data=cmts202011, x="dep")
```
- DataFrame
```python
sb.countplot(ax=ax, x=label_train)
```
- `x`: (Array, List of Arrays)
### `sb.replot()`
```python
ax = sb.replot(x="total_bill", y="tip", col="time", hue="day", style="day", kind="scatter", data=tips)
```
### `sb.kedplot()`
```python
sb.kdeplot(ax=ax, data=data["ppa_root"])
```
### `sb.stripplot()`
```python
ax = sb.stripplot(x=xx, y=yy, data=results_order, jitter=0.4, edgecolor="gray", size=4)
```
### `sb.pairtplot()`
```python
ax = sb.pairplot(data_for_corr)
```