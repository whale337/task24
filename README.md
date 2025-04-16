import dash
import more_itertools
from dash import dcc
from dash import html
from dash.dependencies import Input, Output
import pandas as pd
import plotly.graph_objs as go
import plotly.express as px

###Note from Andrew
#Ive noticed that many of variables aren't define anywhere in the skelelton code or throughout the tasks. Is that what I'm missing? 
# I also dont know why some of the code is getting underlined. I've only used text files and the IBM dash program.


# Load the data using pandas
data = pd.read_csv('https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DV0101EN-SkillsNetwork/Data%20Files/historical_automobile_sales.csv')

# Initialize the Dash app
app = dash.Dash(__name__)

# Set the title of the dashboard
app.title = "Automobile Statistics Dashboard"

app.layout = html.Div(children=[html.H1('Automobile Statistics Dashboard', 
                                style={'textAlign': 'center', 'color': '#503D36',
                                'font-size': 24}),

#TASK 2.2: Add two dropdown menus
    html.Div([
        html.Label("Select Statistics:"),
        dcc.Dropdown(id='dropdown-statistics', 
                    options=[
                           {'label': 'Yearly Statistics', 'value': 'Yearly Statistics'},
                           {'label': 'Recession Period Statistics', 'value': 'Recession Period Statistics'}
                           ],
                    placeholder='Select a report type')]),


	html.Div(dcc.Dropdown(
            id='select-year',
            #options=[{'label': i, 'value': i} for i in year_list]
	    year_list=[i for i in range(1980, 2024, 1)],
            value='Select-year',
            placeholder='Year')),

	html.Div([html.Div(id='output-container', className='chart-grid', style={'display': 'flex'}),])

#TASK 2.4: Creating Callbacks; Define the callback function to update the input container based on the selected statistics and the output container
@app.callback(
    Output(component_id='select-year', component_property='disabled'),
    Input(component_id='dropdown-statistics',component_property='value'))

################SYNTAX ERROR###############################
def update_input_container(input_yr, input_rec):
    if input_yr == 'Yearly Statistics': 
        return False
    else: 
        return True

#after reviewing the practice version I thought it would help if I defined the variables after creating the input container
yr_stats = data[data['Year'] == input_yr]
rec_stats = data[data['Recession' == 1] == input_rec]

@app.callback(
    Output(component_id='output-container', component_property='childen'),
    [Input(component_id='dropdown-statistics', component_property='value'), Input(component_id='select-year', component_property='value')])


def update_output_container(report type, Yearly Statistics):
    if Recession Period Statistics == 'Recession Period Statistics':
        # Filter the data for recession periods
        recession_data = data[data['Recession'] == 1]

#NOTE: Take the screenshot representing the the code snippet wherein you have created the two callback functions and save it as ‘Callbacks.png’

#I realize there is more to the code so I left the rest of it off so we can figure things out by task.

# Run the Dash app
if __name__ == '__main__':
    app.run_server(debug=True)
