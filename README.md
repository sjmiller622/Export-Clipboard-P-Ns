# Export-Clipboard-P-Ns

# -*- coding: utf-8 -*-
"""
Created on Mon May 18 13:49:22 2020

@author: sjmiller
"""

#Put in list type
list_type = input('Is this list for TeamCenter (TC) or Formtek (FTK)?\n_')
if list_type.lower() == 'tc':
    list_type = 'tc'
else:
    list_type = 'ftk'
    
# When pasting in the parts_list from the WU_all,
# move the trailing list to the right as a group (use tab
# to create whitespace for the .split() to work
# then put \ at the end of each line except the 
# last (because it is a ')

#When pasting list into formtek, you will need to 'backspace' and 'space' for some reason.
#It doesn't like the paste (ctrl-V) by itself for some reason.
parts_list = 'P140156\
    P903551\
    P953516\
    G290012\
    H002977'
parts_list = parts_list.split()
count_parts = len(parts_list)
cleaned = ''
if list_type == 'tc': 
    for part_count,item in enumerate(parts_list):
        # Use this line to create the TeamCenter search list
        if part_count == (count_parts - 1):
            cleaned=cleaned+item+':A*,'+item+':W*'
        else:
            cleaned=cleaned+item+':A*,'+item+':W*,'
    print (cleaned,'\n')
    print(f'Total Parts = {count_parts}')
else:   
#Formtek formatting- with an extra space at the end      
    for part_count,item in enumerate(parts_list):
        # Use this line to create the formtek search list
        if part_count == (count_parts - 1):
            cleaned='#IN '+cleaned+item+' '
        else:
            cleaned=cleaned+item+','
    print(cleaned)
