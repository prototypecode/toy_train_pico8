# Toy Train Pico-8

```lua
function _init()
  cls()
  switch_state = 0
  train = {
    {64, 8},
    {72, 8},
    {80, 8}
  }
end
```

```lua

function _init()
   cls()
   switch_state = 0
   train = {{64, 8}, {72, 8}, {80,8}}
end

function move_segments(s, dir)
   spd = dir * 2
   if (s[2] == 8) then
      if(s[1] == 112) then
         s[2] += spd
      else
         s[1] += spd
      end
   else
      if (s[1] == 112) then
         if (s[2] == 112)	then
            s[1] -= spd
         else
            s[2] += spd
         end
      else
         if (s[2] == 112) then
            if (s[1] == 8)	then
               s[2] -= spd
            else
               s[1] -= spd
            end
         else
            if (s[1] == 8) then
               if (s[2] == 8) then
                  s[1] += spd
               else
                  s[2] -= spd
               end
            end
         end
      end
   end
end

function adv_switch()
   if (switch_state < 1) then
      switch_state += 1
   else
      switch_state = 0
   end
end

function move_train()
   for t in all(train) do
      move_segment(t, switch_state)
   end
end

```

