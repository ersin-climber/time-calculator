# getting the input from user
while True:
    try:
        start = input("Enter a start time in 12h format ending in AM or PM (Exp. '10:15 PM'): ")
        if start[-6] != ":":
            print("Error: Invalid format")
            continue
        elif 12 < int(start[:-6]):
            print("Error: Hour must be between 1 and 12!")
            continue
        elif int(start[:-6]) < 1:
            print("Error: Hour must be between 1 and 12!")
            continue
        elif int(start[-5:-3]) < 0:
            print("Error: Minutes must be between 0 and 59")
            continue
        elif 59 < int(start[-5:-3]):
            print("Error: Minutes must be between 0 and 59")
            continue
        elif start[-2:] not in ["AM", "PM"]:
            print("Error: Last two letters should be 'AM' or 'PM'.")
            continue
        else:
            start = start
            print(start)
            break
    except:
        print("Error: Invalid start time format. Please enter again!")
        continue

while True:
    try:
        duration = input("Enter the duration with hours and minutes (Exp. '5:20'): ")
        if int(duration[:-3]) < 0:
            print("Error: Hours should be any whole number")
            print(duration[:-3])
        elif duration[-3] != ":":
            print("Error: Invalid format")
            continue
        elif int(duration[-2:]) < 0:
            print("Error: Minutes must be between 0 and 59")
            continue
        elif 59 < int(duration[-2:]):
            print("Error: Minutes must be between 0 and 59")
            continue
        else:
            duration = duration
            print(duration)
            break
    except:
        print("Error: Invalid duration format! Please enter again!")
        continue

starting_day = ""
while True:
    a = input("Enter the starting day (Optional): ")
    if a == "":
        starting_day = starting_day
        break
    elif a != "":
        starting_day = a.title()
        if starting_day in ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]:
            starting_day = starting_day
            break
        else:
            starting_day = ""
            print("Error: Not a valid day of week!")
            continue

start_rep = start.replace(":", " ")
start_spl = start_rep.split()
duration_spl = duration.split(":")
duration_hour = int(duration_spl[0])
duration_min = int(duration_spl[1])


def add_time(start, duration, starting_day=""):
    start_hour = int(start_spl[0])
    start_min = int(start_spl[1])
    start_am_pm = str(start_spl[2])
    new_hour = start_hour + duration_hour
    new_min = start_min + duration_min

# finding new minutes
    if new_min > 59:
        new_hour = new_hour + 1
        new_min = new_min % 60
        if new_min in range(10):
            new_min = f"0{new_min}"
        else:
            new_min = new_min
    else:
        if new_min in range(10):
            new_min = f"0{new_min}"
        else:
            new_min = new_min

# finding new hours
    if new_hour > 12:
        reminder_new_hour = new_hour % 12
        floor_new_hour = new_hour//12
        if reminder_new_hour == 0:
            new_hour = 12
        else:
            new_hour = reminder_new_hour
        if floor_new_hour % 2 == 0:
            start_am_pm = start_am_pm
        else:
            if start_am_pm == "AM":
                start_am_pm = "PM"
            else:
                start_am_pm = "AM"
    else:
        if new_hour == 12:
            if start_am_pm == "AM":
                start_am_pm = "PM"
            else:
                start_am_pm = "AM"
        else:
            new_hour = new_hour

#  finding the nex day
    next_day = ""
    am_pm_first = str(start_spl[2])
    if am_pm_first == "AM":
        start_time = (start_hour * 60) + start_min
        add_time = (duration_hour*60) + duration_min
        final_time = start_time + add_time
        if 1440 <= final_time < 2880:
            next_day = "(next day)"
        elif final_time >= 2880:
            flr = final_time//1440  # floor value of final time as of 1440 (24h*60min)
            next_day = f"({flr} days later)"
        else:
            next_day = next_day
    else:
        start_time = ((start_hour + 12) * 60) + start_min
        add_time = (duration_hour * 60) + duration_min
        final_time = start_time + add_time
        if 1440 <= final_time < 2880:
            next_day = "(next day)"
        elif final_time >= 2880:
            flr = final_time // 1440
            next_day = f"({flr} days later)"
        else:
            next_day = next_day

#  finding the day of the week
    days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
    if next_day == "":
        if starting_day == "":
            starting_day = starting_day
        else:
            starting_day = f", {starting_day}"
    elif next_day == "(next day)":
        if starting_day == "":
            starting_day = starting_day
        else:
            ind = days.index(starting_day) + 1
            starting_day = f", {days[ind]}"
    else:
        if starting_day == "":
            starting_day = starting_day
        else:
            ind_nex_day_str = next_day[1]
            ind_use_day = days.index(starting_day)
            new_ind = int(ind_nex_day_str) + int(ind_use_day)
            if new_ind < 7:
                new_ind = new_ind
                starting_day = f", {days[new_ind]}"
            else:
                x = (new_ind) % 6
                new_ind_final = x - 1
                starting_day = f", {days[new_ind_final]}"

    print(f"Result is: {new_hour}:{new_min} {start_am_pm}{starting_day} {next_day}")


add_time(start, duration, starting_day)
