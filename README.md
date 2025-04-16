
###Note from Andrew
#Ive noticed that many of variables aren't define anywhere in the skelelton code or throughout the tasks. Is that what I'm missing? 
# I also dont know why some of the code shows up as underlined when I tried to include it in this readme file. I've delete it from this file since it was included in the .py file.


   
################SYNTAX ERROR###############################
def update_input_container(input_yr, input_rec):
    if input_yr == 'Yearly Statistics': 
        return False
    else: 
        return True

#after reviewing the practice version I thought it would help if I defined the variables after creating the input container
yr_stats = data[data['Year'] == input_yr]
rec_stats = data[data['Recession' == 1] == input_rec]

