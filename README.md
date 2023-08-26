# Toy Train Pico-8

![](https://prototypecode.itch.io/toy-train-pico-8)

```lua

--toy train demo
--z to stop and start the train

function _init()
   cls()
   switch_state=0
   train={{64,8},{72,8},{80,8},{88,8}}
end

--

function move_segment(s,dir)
   spd=dir*2
   if(s[2]==8) --top side
   then
      if(s[1]==112) --top right
      then
         s[2]+=spd
      else
         s[1]+=spd
      end
   else
      if(s[1]==112) --right side
      then
         if(s[2]==112) --bottom right
         then
            s[1]-=spd
         else--
            s[2]+=spd
         end
      else
         if(s[2]==112) --bottom side
         then
            if(s[1]==8) --bottom left
            then
               s[2]-=spd
            else
               s[1]-=spd
            end
         else
            if(s[1]==8) --left side
            then
               if(s[2]==8) --top left
               then--
                  s[1]+=spd
               else
                  s[2]-=spd
               end
            end
         end
      end
   end
end

--

function adv_switch()
   if(switch_state<1)
   then
      switch_state+=1
   else
      switch_state=0
   end
end

--

function move_train()

   for t in all(train)
   do
      move_segment(t,switch_state)
   end

end

--

function _update()
   if(btnp(4))
   then
      adv_switch()
   end
   move_train()
end

--

function draw_train()
   for t=1,count(train)
   do
      if(t==1)
      then
         sprite=11
      else
         if(t==count(train))
         then
            sprite=13
         else
            sprite=12
         end
      end
      spr(sprite,train[t][1],
      train[t][2])
   end
end

--

function draw_switch()
   if(switch_state==1)
   then
      sspr(0,16,16,16,56,56,16,16)
   else
      sspr(64,16,16,16,56,56,16,16)
   end
end

--


function _draw()
   mapdraw(0,0,0,0,16,16)
   draw_switch()
   draw_train()
end

```

