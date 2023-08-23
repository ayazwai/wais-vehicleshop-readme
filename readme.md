# How to set it up

- You should read the sql file in the script to the database you use via **phpmyadmin** or **heidisql** 

- 

## Important for ESX!

- Access `es_Extended -> server -> server -> classes -> player.lua`

- `function self.setJob(job, grade)` find this function
Under `self.triggerEvent('esx:setJob', self.job)` write `return true` just like in the photo 

- and put `print(('[es_extended] [^3WARNING^7] Ignoring invalid .setJob() usage for "%s"'):format(self.identifier))` below the code line `return false`

![alt text](https://cdn.discordapp.com/attachments/1035485961217384488/1142817077992902738/image.png)

## Photos not showing!

- You can click here to [download](https://drive.google.com/file/d/1MIE0PpiMfWslGmVSTI1cey43bfe8GKLg/view?usp=drive_link) the photos after downloading:

```
wais-vehicleshop\nui
```
- Drag and drop the public file into the folder

---

## *Config.Devmode*

- Use it only when you want to restart the script. Use when there is maintenance on the server. If it is normally open, the script will not run.

## *Config.TestDriveTime*

- Enter Integer number in seconds. 10, 30, 40
- The last 30 seconds or less than 30 seconds will throw a notification.

## *Config.TestDriveCoords*

- Be careful to enter vector4 location. 

- The players will not see each other as they will teleport to different worlds to the coordinates entered.

## *Config.Unemployed*

- Enter all known details of your unemployed occupation here. Change the value of existing variables.

## *Config.Cash*

- Set the required data here if the coin is an item or not.

---

# *Config.VehicleShops*

- To enter a new buyable shop, create a table structure as in the example and fill in the data.

## *1 - Shop Name*

- This is the shop name that will appear at the entrance of the showroom before and after the purchase. 

- **When you change this table name, you should find the old name in the sql table and update the `shop_name` column with the new version. Otherwise the gallery will be deleted!**

## *2 - Coords*

- Some of the Shop's locations need to be adjusted.

> **boss**: The coordinate from which employees will access the administration panel. Accepts @vector3

> **buy_shop**: It is the coordinate where the business will be purchased. @vector3 accepts.

> **vehicle_shop**: The coordinate where the vehicles will be displayed. @vector3 accepts.

> **ped_hidden**: In the Showrrom, you have to hide the pad behind a wall or a certain spot. @vector3 accepts.

> **car_coords**: The coordinates of the vehicle that will be displayed in the showroom. @vector3 accepts.

> **car_rotation**: The rotation of the vehicle that will be displayed in the showroom. @float accepts.

> **camera**: The camera that will be displayed in the showroom. @table accepts.

> **spotlight**: The spotlight that will be displayed in the showroom. @table accepts.

> **buyed_spawn**: The coordinates of the vehicle that will be displayed in the showroom after the business is purchased. @vector3 accepts.

## *3 - Jobs*

- **It is important! that the content and necessary information of the jobs that people will have when the business is purchased should be set here**

> **name**: The name of the job that will be created when the business is purchased. @string accepts

> If you are using ESX, you should open your SQL program and go to the jobs table and then enter the job name of this shop. You can do anything you want. You have to write the name you put in the name section properly

> QB If you are using an infrastructure, you should create a new table from qb-core -> shared -> jobs.lua and enter the required information just like in the example

```
["vehshop_a"] = {
    label = 'Car Dealership - A',
    defaultDuty = true,
    grades = {
        ['1'] = {
            name = 'employees',
            payment = 50
        },
        ['2'] = {
            name = 'assistant',
            payment = 100
        },
        ['3'] = {
            name = 'owner',
            payment = 150
        },
    },
}
```

> **boss_grade**: The grade that will be the boss of the business. @integer accepts

> **grades**: The grades that will be created when the business is purchased. @table accepts

- > **grade_name**: The name of the grade that will be created when the business is purchased. @string accepts

- > **person_page**: The permissions that will be given to the person page that will be created when the business is purchased. @table accepts

- > **stock_page**: The permissions that will be given to the stock page that will be created when the business is purchased. @table accepts

- > **settings_page**: The permissions that will be given to the settings page that will be created when the business is purchased. @boolean accepts

## *4 - Categorys*

- Categories can be changed from shop to shop. These categories and the vehicles in it are set from the vehicles.lua file.
- ["Name of the categorization to appear"] = "value of the categorization"

## *5 - Components*

- **It is important! that the content and necessary information of the components that will be created when the business is purchased should be set here**

> **banner**: The banner that will be displayed in the showroom. @string accepts

> **logo**: The logo that will be displayed in the showroom. @string accepts

> **blips_id**: The blips id that will be displayed in the showroom. @integer accepts

> **blips_name**: The blips name that will be displayed in the showroom. @string accepts

> **blips_color**: The blips color that will be displayed in the showroom. @integer accepts

## *6 - Settings*

- **It is important! that the content and necessary information of the settings that will be created when the business is purchased should be set here**

> **max_employees**: The maximum number of employees that can be hired. @integer accepts

> **rent_day**: The number of days the business will be rented. @integer accepts

> **rent_price**: The price of the business to be rented. @integer accepts

> **text**: The text that will be displayed when the player is in the boss area. @string accepts

> **text_entershop**: The text that will be displayed when the player is in the showroom. @string accepts

```
["Shop Name"] = {
    ["coords"] = {
        ["boss"] = vector3
        ["buy_shop"] = vector3
        ["vehicle_shop"] = vector3
        ["ped_hidden"] = vector3
        ["car_coords"] = vector3
        ["car_rotation"] = 0.0
        ["camera"] = {
            ["type"] = "DEFAULT_SCRIPTED_CAMERA",
            ["cam_defaultCoords"] = vector3
            ["rotateZ"] = 0.0
            ["pov"] = 0.0
            ["rot"] = 0.0
        },
        ["spotlight"] = {
            use = true, -- If you make it false, the lights will be on in the showroom.
            x = 0.0, 
            y = 0.0, 
            z = 0.0,
            rotation = 0.0,
            distance = 0.0,
            radius = 0.0,
        },
        ["buyed_spawn"] = vector3
    },
    ["jobs"] = {
        ["name"] = "vehshop_a"
        ["boss_grade"] = 3
        ["grades"] = {
            ["3"] = {
                ["grade_name"]    = "Owner",
                ["person_page"]   = {
                    ["hire"] = true,
                    ["fire"] = true,
                    ["upgrade"] = true,
                    ["downgrade"] = true,
                },
                ["stock_page"]    = {
                    ["edit_price"] = true,
                    ["add_stock"] = true,
                },
                ["settings_page"] = true,
            },
            ["2"] = {
                ["grade_name"]    = "Assistant",
                ["person_page"]   = {
                    ["hire"] = true,
                    ["fire"] = true,
                    ["upgrade"] = false,
                    ["downgrade"] = true,
                },
                ["stock_page"]    = {
                    ["edit_price"] = true,
                    ["add_stock"] = true,
                },
                ["settings_page"] = false,
            },
            ["1"] = {
                ["grade_name"]    = "Employee",
                ["person_page"]   = false,
                ["stock_page"]    = false,
                ["settings_page"] = false,
            },
        }
    },
    ["categorys"] = {
        ["Compacts"] = "compacts",
        ["Sedans"] = "sedans",
        ["SUVs"] = "suvs",
        ["Coupes"] = "coupes",
        ["Muscle"] = "muscle",
        ["Sports Classics"] = "sportsclassics",
        ["Sports"] = "sports",
        ["Super"] = "super",
        ["Motorcycles"] = "motorcycles",
        ["Off-road"] = "offroad",
        ["Vans"] = "vans",
        ["Cycles"] = "cycles",
    },
    ["employees"] = {}, -- Don't touch
    ["vehicles"] = {}, -- Don't touch
    ["logs"] = {}, -- Don't touch
    ["components"] = { --Data that comes by default when the business is rented.
        ["banner"] = "https://i1.sndcdn.com/visuals-000479340132-gGD9WT-original.jpg",
        ["logo"] = "https://mikekim.com/wp-content/uploads/2017/01/logo-here.png",
        ["blips_id"] = 1,
        ["blips_name"] = "Vehicleshop",
        ["blips_color"] = 1,
        ["money"] = 0
    },
    ["settings"] = {
        ["buyed"] = false, -- Don't touch
        ["max_employees"] = 5,
        ["rent_day"] = 30,
        ["remaining_day"] = 0, -- Don't touch
        ["rent_price"] = 1000,
        ["text"] = "[E] - Open Boss Menu",
        ["text_entershop"] = "[E] - Enter to shop %s",
    },
    ["buy_settings"] = {
        ["text"] = "[E] - Buy car dealership %s for $%s price",
        ["distance"] = 2.5,
    }
}
```