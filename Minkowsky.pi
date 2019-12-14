# -*- coding: utf-8 -*-
"""
Created on Wed Dec 11 13:06:46 2019

@author: bart.bozon
"""
import matplotlib.pyplot as plt
import math
savefigteller=0

class Minkowski_diagram :
    def __init__(self):
        self.canvassize_x=12
        self.canvassize_y=6
        self.size_x=20
        self.size_y=10
        self.worldline_v=[]
        self.worldline_x=[]
        self.worldline_color=[]
        self.worldline_time_axis=[]
        self.worldline_time_null=[]
        self.lightcircle_x=[]
        self.lightcircle_t=[]
        self.lightcircle_color=[]
        self.spacetimehyperbola=[]
        self.relativespeed=0
    def LTX(self,x,t):
        LT_x=(x-self.relativespeed*t)*1/math.sqrt(1-self.relativespeed**2)
        return LT_x
    def LTT(self,x,t):
        LT_t=(t-self.relativespeed*x)*1/math.sqrt(1-self.relativespeed**2)
        return LT_t
    def ILTT(self,x,t,v):
        ILT_t=t*math.sqrt(1-v**2)+v*x
        return ILT_t
    def ILTX(self,x,t,v):
        ILT_x=x*math.sqrt(1-v**2)+v*t
        return ILT_x
    def define_spacetime_hyperbola(self,spacetime_distance_squared):
        self.spacetimehyperbola.append(spacetime_distance_squared)
    def define_wordline(self,x,v,color,axis,time_null):
        self.worldline_v.append(v)
        self.worldline_x.append(x)
        self.worldline_color.append(color)
        self.worldline_time_axis.append(axis)
        self.worldline_time_null.append(time_null)
    def define_lightcircle(self,t,x,color):
        self.lightcircle_x.append(x)
        self.lightcircle_t.append(t)
        self.lightcircle_color.append(color)
    def set_frame_of_reference(self,v):
        self.relativespeed=v
    def show(self):
         global savefigteller
         plt.rcParams["figure.figsize"] = (self.canvassize_x,self.canvassize_y)
         plt.xlim(-self.size_x/2,self.size_x/2)    
         plt.ylim(0,self.size_y)
         plt.xlabel('x ->')
         plt.ylabel('t->')
         gamma=1/math.sqrt(1-self.relativespeed**2)
         data_x=[]
         data_min_x=[]
         data_y=[]
         for t in range (0,self.size_y*25,1):
             data_x.append(t/25)
             data_min_x.append(-t/25)
             data_y.append(t/25)
         plt.scatter(data_x,data_y,c='y',s=1)
         plt.scatter(data_min_x,data_y,c='y',s=1)
         for i in range (len(self.spacetimehyperbola)):
             data_x=[]
             data_y=[]
             if self.spacetimehyperbola[i]>0:
                 for k in range (-self.size_x*4,self.size_x*4):
                  data_x.append(k/4)
                  data_y.append(math.sqrt(self.spacetimehyperbola[i]+(k/4)**2))
             else:
                 for k in range (0,self.size_y*4):
                  data_y.append(k/4)
                  data_x.append(math.sqrt(-self.spacetimehyperbola[i]+(k/4)**2))
             plt.scatter(data_x,data_y,c="k",s=2)
         for i in range (len(self.worldline_v)):
             data_x=[]
             data_y=[]
             if self.worldline_time_axis[i]=='yes':
                 for k in range (-self.size_x,self.size_x):
                   for l in range (0,5):
                     j=k+l/20
                     v=self.ILTT(j,self.worldline_time_null[i],self.worldline_v[i])
                     x=self.LTX(j,v)
                     t=self.LTT(j,v)
                     data_x.append(x)
                     data_y.append(t)
                 plt.scatter(data_x,data_y,c=self.worldline_color[i],s=1)
                 v=self.ILTT(-1,self.worldline_time_null[i],self.worldline_v[i])
                 x=self.LTX(-1,v)
                 t=self.LTT(-1,v)
                 if (t<self.size_y) and (t>0):
                  plt.text (x,t+0.1,'t='+str(self.worldline_time_null[i]))

             t_max = self.LTT(self.worldline_x[i]+self.worldline_v[i]*self.size_y,self.size_y)   
             data_x=[]
             data_y=[]
             for j in range (0,int(self.size_y*self.size_y/t_max*100),int(self.size_y*self.size_y/t_max*100/50)):
                 t = self.LTT(self.worldline_x[i]+self.worldline_v[i]*j/100,j/100)   
                 x = self.LTX(self.worldline_x[i]+self.worldline_v[i]*j/100,j/100)   
                 data_x.append(x)
                 data_y.append(t)
             plt.scatter(data_x,data_y,c=self.worldline_color[i],s=1)
             if self.worldline_x[i]==0 :
                 plt.text (x,t+0.3,'v='+str(self.worldline_v[i])+"c")
         for i in range (len(self.lightcircle_x)):
             x=self.LTX(self.lightcircle_x[i],self.lightcircle_t[i])
             t=self.LTT(self.lightcircle_x[i],self.lightcircle_t[i])
             data_x=[]
             data_min_x=[]
             data_y=[]
             for j in range (int(t*1000),self.size_y*1000,50):
                 data_x.append(x+j/1000-t)
                 data_min_x.append(x-j/1000+t)
                 data_y.append(j/1000)
             plt.scatter(data_x,data_y,c=self.lightcircle_color[i],s=1)
             plt.scatter(data_min_x,data_y,c=self.lightcircle_color[i],s=1)
             plt.scatter(x,t,marker="x",c="k")
         plt.text (-self.size_x/2+1,0.5,'vref='+str(self.relativespeed)+"c")
         fname = 'MIN%04d.png' % savefigteller
         plt.savefig(fname)
         savefigteller=savefigteller+1
         plt.show()  

##-----------------------------------------------------
# Manual Minkoswki_diagram
# 
# each time a worlddiagram is made a png file is saved to the HD.
# with makeavi (freeware) a movie can be made of the sequence of png's
#          
# Methods:
#
# define_spacetimehyperbola (s^2)
# is used to create a (curved) line with a constant s^2 
# spacetime is defined as: s^2=-(ct)^2+x^2+y^2+z^2         
#
# define_wordline(x,v,color,constant_time_line,time_null)
# is used to create a worldline
# x : the position (in vref=0c) of the worldline at t=0
# v : the speed versus the reference frame vref=0c
# color : color of line (applies also for constant time line)
# constant_time_line : if "yes" a constant time line is depicter with: time = time_null
#
# define_lightcircle(t,x,color)
# is used to create an event
# x :  the position (in vref=0c) of the event
# t :  the time (in vref=0c) of the event
# color : the color of the lightcone of the event
#         
# set_frame_of_refernce(v):
# is used to shift the frame of reference to speed v
#
##-----------------------------------------------------
       
M=Minkowski_diagram()

# the scenarios below can be turned on in spyder by selecting 
# one scenario and pressing ctrl+1

##-----------------------------------------------------
## scenario in which 6 worldlines are created in which each worldline has a delta v of 0.5 c to the line next to it.
#M.define_wordline(0,0,'r','no',5)
#M.define_wordline(0,0.5,'r','no',5)
#M.define_wordline(0,0.8,'r','no',2)
#M.define_wordline(0,0.928571,'r','no',2)
#M.define_wordline(0,0.97561,'r','no',2)
#M.define_wordline(0,0.991803,'r','no',2)
#for i in range (0,970,10):
#    print(i)
#    M.set_frame_of_reference(i/1000)
#    M.show() 
##-----------------------------------------------------

##-----------------------------------------------------
## scenario in which 4 events are created. The lightcones of the first 3 events all
## come together at the 4th event. In the animation it is shown that 
##simultaneity is different for different reference frames.    
#M.define_lightcircle(5,2,'#fbfb00')
#M.define_lightcircle(5,0.7*5,'#fbfb00')
#M.define_lightcircle(5-3.35,-1.35,'#fbfb00')
## three events are created
#M.show()
#M.define_lightcircle(5.75,2.75,'#fbfb00')
#M.show()
#M.define_wordline(0,0.7,'b','yes',3.65)
#M.define_wordline(0,0,'r','yes',5)
#M.show() 
#for i in range (0,710,10):
#    print(i)
#    M.set_frame_of_reference(i/1000)
#    M.show() 
##-----------------------------------------------------

##-----------------------------------------------------
# Last scenario. Explanation is given in print
M.define_lightcircle(0,0,'#fbfb00') # the centre
M.define_lightcircle(5,2,'#fbfb00') # the left event
M.define_lightcircle(5,0.7*5,'#fbfb00') # the right event
M.define_lightcircle(5.75,2.75,'#fbfb00') # where the light comes together
M.show() 
print ('2 events which lightcone intersects at the third event')
M.define_lightcircle(1,4,'#ffff00') # an event outside the x=0/t=0-lightcone
M.show() 
print ('An event outside the lightcone of the origin')
M.define_wordline(0,0,'m','no',5)  
M.show() 
print ('Added worldline with v=0c')
M.define_wordline(0,0.47,'b','no',3.8)
M.show() 
print ('Added worldline with v=0.47c')
M.worldline_time_axis[0]="yes"
M.show() 
print ('Turned on the constant time axis (t=5) for first worldline')
M.worldline_time_axis[1]="yes"
M.show() 
print ('Turned on the constant time axis (t=3.8) for second worldline')
M.set_frame_of_reference(0.47)
M.show()   
print ('Changed refernence frame speed so that second worldline is now vertical.')
print ('Please note the event outside the light cone is now below t=0')
M.define_spacetime_hyperbola(5**2-(0.7*5)**2)
M.show() 
print ('Turned on the space time hyperbola for 1st event')
print ('The events glide over this line if Vref changes...')
M.set_frame_of_reference(0)
M.show()   
print ('Changed refernence frame speed')
M.define_spacetime_hyperbola(1**2-4**2)
M.show()
print ('Turned on the space time hyperbola for event outside of lightcone')
M.set_frame_of_reference(0.7)
M.show()   
print ('Changed refernence frame speed again. It is clear to see that events ')
print ('with spacetime separation <0 (e.g. the centre and the event outside')
print ('the light cone) the order of the events is not determined. It')
print ('depends on the velocity/speed of the reference frame.')
##-----------------------------------------------------
