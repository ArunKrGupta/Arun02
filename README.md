Arun02
======
import csv


csv_out = open("C:\\logfile.csv", 'wb')
## create the csv writer object.
mywriter = csv.writer(csv_out)

Presenters_Name_List = [] 
Presenters_Time_List = [] 
Presenters_Charge_List = [] 
Presenters_details = [] 
    

dictionary = {}

hoursList = []

def ReadFromCSVFile():
    CSVList= []

    with open("C:\\csvfile.csv", 'rb') as f:
        reader = csv.reader(f)
        #csvlist = reader
        row1 = ""
        for x in reader:
            
            row = x
            print " row1"+str(row1)
            # print row1
            #row = row.split(',')
            print row
            CSVList.append(row)
            print(str(row[0]))
            Presenters_name = str(row[0])
            Presenters_Name_List.append(Presenters_name)
             
            print(str(row[1]))
            Presenters_time = str(row[1])
            Presenters_Time_List.append(Presenters_time) 
            
            print(str(row[2]))
            Presenters_price = str(row[2])
            Presenters_Charge_List.append(Presenters_price)
            
            hoursList.append(int(Presenters_time))
            dictionary[int(Presenters_time)] = [str(Presenters_name),int(Presenters_price)]

    f.close()

def NoOfCombination (prefix, list, count): 
    #index2 = index2+1
    if count is 0: 
        list1.append(prefix)
        #return prefix
    for i in range (len(list)): 
        NoOfCombination("%s%s"%(prefix,list[i]), list[i+1:], count - 1) 
        
index1 = 0
index2 = 0
list1 = []
# Call Read From csv function
ReadFromCSVFile()

# Find number of combinations
NoOfCombination("", hoursList, 3)
print " Combinations list is: "+ str(list1)
combinations = len(list1)
mainList  = []
print " number of combinations are "+ str(combinations)
costlist = []
durationList = []
for item in range(0,combinations):
    combination = list1[item]
    totalhours = 0
    totalprice = 0
    presentersNames =[]
    for i in combination:
        #print " price for the : "+ str(dictionary[int(i)][0]) +" is:"+ str(dictionary[int(i)][1])
        presentersNames.append(str(dictionary[int(i)][0]))
        totalhours = totalhours + int(i)## To get price of the particular hour from dictionary
        totalprice = totalprice + dictionary[int(i)][1]
    if(totalhours <= 8):
            mainList.append(combination)
            mainList.append(totalhours)
            mainList.append(totalprice)
            mainList.append(presentersNames)
            costlist.append(totalprice)
            durationList.append(totalhours)
           
print " Number of combinations with less than or equal to 8 hours is:" + str(len(costlist))
        
print "total price: "+ str(totalprice)
print " Main List is: " + str(mainList)

 ###################Case 1: Minimum Cost ##########################################
print "Case1 ---------------------------------------------------------------------"
mincost = min(costlist)
print "minimum cost in the selecetd combinatios are :"+ str(mincost)

index = mainList.index(mincost)
print " combination" + str(mainList[index-2])
print " prsenters Names " + str(mainList[index+1])
print " hours" + str(mainList[index-1])
print " cost" + str(mainList[index])

######################Case 2 : Maximum  hours presentation #########################
print "Case2 ---------------------------------------------------------------------"
maxhours = max(durationList)
print "maximum hours presentation in selected combinatiomns are:" + str(maxhours)
index = mainList.index(maxhours)
print " combination" + str(mainList[index-1])
print " hours" + str(mainList[index])
print " cost" + str(mainList[index+1])
print " prsenters Names " + str(mainList[index+2])






        

