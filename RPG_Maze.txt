def showInstructions():
  print('''
RPG Game
========

You are a an army person, you have to collect all the things which are there in the Terrorist base.

Get to the num15 room with the bombs, guns, gold, money, key and laptop. 
Avoid the Terrorists!
All the Best !

Commands:
  go [direction]
  get [item]
''')

def showStatus():
  print('---------------------------')
  print('You are in the ' + currentRoom)
  print('Inventory : ' + str(inventory))
  if "item" in rooms[currentRoom]:
    print('You see a ' + rooms[currentRoom]['item'])
  print("---------------------------")

inventory = []

rooms = {

            'Hall' : {
                'south' : 'num4',
                'east' : 'num2'
                },

            'num2' : {
                'east' : 'num3',
                'west' : 'Hall',
                'south' : 'num5'
                },
            
            'num3' : {
                'west' : 'num2',
                'south' : 'num6',
                'item' : 'terr'
                },
            
            'num4' : {
                'north' : 'Hall',
                'east' : 'num5',
                'south' : 'num7',
                'item' : 'bombs'
                },
            
            'num5' : {
                'north' : 'num2',
                'east' : 'num6',
                'south' : 'num8',
                'west' : 'num4',
                'item' : 'guns'
                },
            
            'num6' : {
                'north' : 'num3',
                'west' : 'num5',
                'south' : 'num9',
                'item' : 'terr'
                },
            
            'num7' : {
                'north' : 'num4',
                'east' : 'num8',
                'south' : 'num11',
                'item' : 'terr'
                },
            
            'num8' : {
                'north' : 'num5',
                'east' : 'num9',
                'south' : 'num12',
                'west' : 'num7',
                'item' : 'gold'
                },
            
            'num9' : {
                'north' : 'num6',
                'east' : 'num10',
                'south' : 'num13',
                'west' : 'num8',
                'item' : 'money'
                },
            
            'num10' : {
                'south' : 'num14',
                'west' : 'num9',
                'item' : 'key'
                },
            
            'num11' : {
                'north' : 'num7',
                'east' : 'num12'
                },
            
            'num12' : {
                'north' : 'num8',
                'east' : 'num11',
                'west' : 'num13',
                'item' : 'terr'
                },
            
            'num13' : {
                'north' : 'num9',
                'south' : 'num15',
                'east' : 'num12',
                'west' : 'num14',
                'item' : 'laptop'
                },
            
            'num14' : {
                'north' : 'num10',
                'west' : 'num13'
                },
            
            'num15' : {
                'north' : 'num13'
                }

         }

currentRoom = 'Hall'

showInstructions()

while True:
  showStatus()
  
  move = ''
  while move == '':  
    move = input('>')
    
  move = move.lower().split()

  if move[0] == 'go':
    if move[1] in rooms[currentRoom]:
      currentRoom = rooms[currentRoom][move[1]]
    else:
        print('You can\'t go that way!')

  if move[0] == 'get' :
    if "item" in rooms[currentRoom] and move[1] in rooms[currentRoom]['item']:
      inventory += [move[1]]
      print('You got ' + move[1])
      del rooms[currentRoom]['item']
    else:
      print('Can\'t get ' + move[1] + '!')

  if 'item' in rooms[currentRoom] and 'terr' in rooms[currentRoom]['item']:
      print('A terrorist has caught you! Game Over !!!')
      break
  if currentRoom == 'num15' and 'key' in inventory and 'guns' in inventory and 'bombs' in inventory and 'gold' in inventory and 'money' in inventory and 'laptop':
      print('You are out of the Building! You Win !!!')
      break
      
