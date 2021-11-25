# Oluwatimileyin Soyege
# Mrs Cotcher
# Computer Science 30
# September 22 2021- Started Menu
# September 29 2021- Finished Menu
# October 6 2021- Started on Inventory
# October 13 2021- Finished Inventory
# October 14 2021- Started on Module and Map
# November 9 2021- Finished Module and Maps
# November 10 2021- Started Exception
# November 12 2021- Finished Exception
# November 16 2021- Started RPG Classes
# November 24 2021- Finished RPG Classes





#-------------------------------------------------


def showInstructions():
  #print a main menu and the commands
  print('''
RPG Game
========

You have found the location of the person who killed your family, but you don't know the exact spot and don't have a GPS in your car, find a way to drive to the location before his plan for department to the Bahamas, you have 15 minutes 



Commands:
  go [direction]
  get [destination]
''')

def showStatus():
  #print the player's current status
  print('---------------------------')
  print('You are currently on ' + status)
  #print the current inventory
  print('Inventory : ' + str(inventory))
  
  
  
  #print an item if there is one
  if "destination" in roads[status]:
    print('Drive to ' + roads[status]['destination'])
  print("---------------------------")

#an inventory, which is initially empty
inventory = []

# this is a dictionary linking a road to other roads
roads = {

            'Eagle Street' : { 
                  'south' : '2nd Avenue',
                  'east'  : '3rd Avenue',
                  'destination'  : '2nd Avenue'
                },

            '2nd Avenue' : {
                  'north' : 'Eagle Street',
                  'east'  : '3rd Avenue',
                  'destination'  : '3rd Avenue'
                },
            '3rd Avenue' : {
                  'west'  : 'Eagle Street',
                  'south' : 'Adam Crescent',
                  'destination'  : 'Adam Crescent'
                },
            'Adam Crescent' : {
                  'north' : '3rd Avenue',
                  'west'  : '2nd Avenue',
                  'east'  : 'Killer Location',
                  'destination'  : 'Killer Location'
                },
            'Killer Location' : {
                  'west'  : 'Adam Crescent'
            }

         }

#  map of all the available roads to get to
def road_map():

  # Makes sure that a variable defaults to an empty string...
  # ...if the current roads doesnt link to another room in that direction.
  try:
    north = rooms[status]['north']
  except:
    north = ""
  try:
    south = rooms[status]['south']
  except:
    south = ""
  try:
    east = rooms[status]['east']
  except:
    east = ""
  try:
    west = rooms[status]['west']
  except:
    west = ""

  # Prints the map
  n = "N"
  s = "S"
  vert_line = "|"
  hzt_line = "-- W -- X -- E --"
  print(north.center(30))
  print("")
  print(vert_line.center(30))
  print(n.center(30))
  print(vert_line.center(30))
  print(west + hzt_line.center(30 - len(west) * 2) + east)
  print(vert_line.center(30))
  print(s.center(30))
  print(vert_line.center(30))
  print("")
  print(south.center(30))
  print("")

#start the player on Eagle Street, address of the player's residency

status = 'Eagle Street'

showInstructions()

#loop forever
while True:
  road_map()
  showStatus()

  #get the player's next 'move'
  #.split() breaks it up into an list array
  #eg typing 'go east' would give the list:
  #['go','east']
  move = ''
  while move == '':  
    move = input('>')

  move = move.lower().split()

  #if they type 'go' first
  if move[0] == 'go':
    #make sure that they are allowed wherever they want to go
    if move[1] in roads[status]:
      #we move from the current road to the next one
      status = roads[status][move[1]]
  
    else:
        print('You are going the wrong way, turn back your car now!')

 

  # in order for the player to win, he will need to these roads/streets in exact order, to reach the killers location
  if status == 'Killer Location' :
    print('You have found the killers location... YOU WIN!')
    break


