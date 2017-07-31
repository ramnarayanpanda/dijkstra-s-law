# dijkstra-s-law
to find shortest path between nodes using dijkstra's law


#d={('1','2'):7, ('1','3'):9, ('1','6'):14, ('2','3'):10, ('2','4'):15, ('3','4'):11, ('3','6'):2, ('6','5'):9, ('5','4'):6}

d={}
s = [[0, 4, 0, 0, 0, 0, 0, 8, 0],
     [4, 0, 8, 0, 0, 0, 0, 11, 0],
     [0, 8, 0, 7, 0, 4, 0, 0, 2],
     [0, 0, 7, 0, 9, 14, 0, 0, 0],
     [0, 0, 0, 9, 0, 10, 0, 0, 0],
     [0, 0, 4, 14, 10, 0, 2, 0, 0],
     [0, 0, 0, 0, 0, 2, 0, 1, 6],
     [8, 11, 0, 0, 0, 0, 1, 0, 7],
     [0, 0, 2, 0, 0, 0, 6, 7, 0]]
     
source=input('enter source')
end=input('enter destination')

for i in range(len(s[0])):
    for j in range(len(s[0])):
        if s[i][j] != 0:
            d[(str(i),str(j))]=s[i][j]
key_list=list(d.keys())

hp_map={}
for i in range(len(s[0])):
    hp_map[str(i)]=1000

dist_map={}
dist_map[source]=0

path_map={}
path_map[source]='null'


def func(current):
    global d,value_list,key_list,hp_map,dist_map,path_map

    connect_list=[i for i in key_list if ((i[0]==current or i[1]==current) and(len([x for x in hp_map.keys() if i[0]==x or i[1]==x])))]

    for i in connect_list:
        j=[x for x in i if x!=current]
        if d[i]+dist_map[current]<hp_map[j[0]]:
            hp_map[j[0]]=d[i]+dist_map[current]
            path_map[j[0]]=current

    min_in_hp_map=min([x for x in hp_map.values()])
        
    for key,value in hp_map.items():
        if value==min_in_hp_map:
            if key==end:
                new_current=key
                break
            new_current=key
            dist_map[key]=min_in_hp_map
            del hp_map[key]
            break
        
    if k==1:
        del hp_map[current]

    return new_current


k=1
if __name__ == '__main__':
    while len(hp_map)>1:
        source=func(source)
        if source==end:
            break
        k=2

x=''
i=end
while True:
    if path_map[i]=='null':
        break
    x+=path_map[i]
    i=path_map[i]

print('shortest path is:','->'.join(x[::-1]+end))
print('minimum length is:',hp_map[end])

