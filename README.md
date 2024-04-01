# Ydata Profiling
## (Generate profile report for  Dataset)
The major purpose of ydata-profiling is to deliver a one-line Exploratory Data Analysis (EDA) experience that is consistent and fast.\
Like the useful pandas df.describe() function, ydata-profiling provides an extended examination of a DataFrame while allowing the data \
analysis to be exported in other forms such as html and json.

<h3>Install</h3>
<pre lang=cmd>pip install ydata-profiling
</pre>
<p>or</p>
<pre lang=cmd>conda install -c conda-forge ydata-profiling
</pre>
<h3>Start profiling</h3>
<p>Start by loading your pandas <code>DataFrame</code> as you normally would, e.g. by using:</p>
<pre lang=python3><span class=kn>import</span> <span class=nn>numpy</span> <span class=k>as</span> <span class=nn>np</span>
<span class=kn>import</span> <span class=nn>pandas</span> <span class=k>as</span> <span class=nn>pd</span>
<span class=kn>from</span> <span class=nn>ydata_profiling</span> <span class=kn>import</span> <span class=n>ProfileReport</span>

<span class=n>df</span> <span class=o>=</span> <span class=n>pd</span><span class=o>.</span><span class=n>DataFrame</span><span class=p>(</span><span class=n>np</span><span class=o>.</span><span class=n>random</span><span class=o>.</span><span class=n>rand</span><span class=p>(</span><span class=mi>100</span><span class=p>,</span> <span class=mi>5</span><span class=p>),</span> <span class=n>columns</span><span class=o>=</span><span class=p>[</span><span class=s2>"a"</span><span class=p>,</span> <span class=s2>"b"</span><span class=p>,</span> <span class=s2>"c"</span><span class=p>,</span> <span class=s2>"d"</span><span class=p>,</span> <span class=s2>"e"</span><span class=p>])</span>
</pre>
<p>To generate the standard profiling report, merely run:</p>
<pre lang=python3><span class=n>profile</span> <span class=o>=</span> <span class=n>ProfileReport</span><span class=p>(</span><span class=n>df</span><span class=p>,</span> <span class=n>title</span><span class=o>=</span><span class=s2>"Profiling Report"</span><span class=p>)</span>
</pre>
<h2>📊 Key features</h2>
<ul>
<li><strong>Type inference</strong>: automatic detection of columns' data types (<em>Categorical</em>, <em>Numerical</em>, <em>Date</em>, etc.)</li>
<li><strong>Warnings</strong>: A summary of the problems/challenges in the data that you might need to work on (<em>missing data</em>, <em>inaccuracies</em>, <em>skewness</em>, etc.)</li>
<li><strong>Univariate analysis</strong>: including descriptive statistics (mean, median, mode, etc) and informative visualizations such as distribution histograms</li>
<li><strong>Multivariate analysis</strong>: including correlations, a detailed analysis of missing data, duplicate rows, and visual support for variables pairwise interaction</li>
<li><strong>Time-Series</strong>: including different statistical information relative to time dependent data such as auto-correlation and seasonality, along ACF and PACF plots.</li>
<li><strong>Text analysis</strong>: most common categories (uppercase, lowercase, separator), scripts (Latin, Cyrillic) and blocks (ASCII, Cyrilic)</li>
<li><strong>File and Image analysis</strong>: file sizes, creation dates, dimensions, indication of truncated images and existence of EXIF metadata</li>
<li><strong>Compare datasets</strong>: one-line solution to enable a fast and complete report on the comparison of datasets</li>
<li><strong>Flexible output formats</strong>: all analysis can be exported to an HTML report that can be easily shared with different parties, as JSON for an easy integration in automated systems and as a widget in a Jupyter Notebook.</li>
</ul>
<p>The report contains three additional sections:</p>
<ul>
<li><strong>Overview</strong>: mostly global details about the dataset (number of records, number of variables, overall missigness and duplicates, memory footprint)</li>
<li><strong>Alerts</strong>: a comprehensive and automatic list of potential data quality issues (high correlation, skewness, uniformity, zeros, missing values, constant values, between others)</li>
<li><strong>Reproduction</strong>: technical details about the analysis (time, version and configuration)</li>    

<h3>Using inside Jupyter Notebooks</h3>
<p>There are two interfaces to consume the report inside a Jupyter notebook: through widgets and through an embedded HTML report.</p>
<img alt="Notebook Widgets" src="https://pypi-camo.freetls.fastly.net/52a2509450f7c7fb10139c6b48986732c252beb8/68747470733a2f2f79646174612d70726f66696c696e672e79646174612e61692f646f63732f6d61737465722f6173736574732f776964676574732e676966" width=800>
<p>The above is achieved by simply displaying the report as a set of widgets. In a Jupyter Notebook, run:</p>
<pre lang=python3><span class=n>profile</span><span class=o>.</span><span class=n>to_widgets</span><span class=p>()</span>
</pre>
<p>The HTML report can be directly embedded in a cell in a similar fashion:</p>
<pre lang=python3><span class=n>profile</span><span class=o>.</span><span class=n>to_notebook_iframe</span><span class=p>()</span>
</pre>
<img alt=HTML src="https://pypi-camo.freetls.fastly.net/26604fdd4c8c21b0d9558d33b0b906a6c9812b52/68747470733a2f2f79646174612d70726f66696c696e672e79646174612e61692f646f63732f6d61737465722f6173736574732f696672616d652e676966" width=800>
<h3>Exporting the report to a file</h3>
<p>To generate a HTML report file, save the <code>ProfileReport</code> to an object and use the <code>to_file()</code> function:</p>
<pre lang=python3><span class=n>profile</span><span class=o>.</span><span class=n>to_file</span><span class=p>(</span><span class=s2>"your_report.html"</span><span class=p>)</span>
</pre>
<p>Alternatively, the report's data can be obtained as a JSON file:</p>
<pre lang=python3><span class=c1># As a JSON string</span>
<span class=n>json_data</span> <span class=o>=</span> <span class=n>profile</span><span class=o>.</span><span class=n>to_json</span><span class=p>()</span>

<span class=c1># As a file</span>
<span class=n>profile</span><span class=o>.</span><span class=n>to_file</span><span class=p>(</span><span class=s2>"your_report.json"</span><span class=p>)</span>
</pre>
<h3>Using in the command line</h3>
<p>For standard formatted CSV files (which can be read directly by pandas without additional settings), the <code>ydata_profiling</code> executable can be used in the command line. The example below generates a report named <em>Example Profiling Report</em>, using a configuration file called <code>default.yaml</code>, in the file <code>report.html</code> by processing a <code>data.csv</code> dataset.</p>
<pre lang=sh>ydata_profiling<span class=w> </span>--title<span class=w> </span><span class=s2>"Example Profiling Report"</span><span class=w> </span>--config_file<span class=w> </span>default.yaml<span class=w> </span>data.csv<span class=w> </span>report.html
</pre>
