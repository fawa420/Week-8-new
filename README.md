boats_hired = 0
total_time_raw = 0
total_time_adjusted = 0
total_amount = 0
boat_usage = [0] * 10

while True:
    hire_boat = input("Do you want to hire a boat? (yes/no): ")

    if hire_boat.lower() == "yes":
        while True:
            boat_number = int(input("Which boat do you want to hire (1-10)? "))
            if 1 <= boat_number <= 10:
                break
            else:
                print("Invalid boat number. Please enter a number between 1 and 10.")

        while True:
            time_choice = input("Do you want to hire the boat for 1 hour or half an hour? (1/half): ")
            if time_choice.lower() == "1":
                time = 1
                break
            elif time_choice.lower() == "half":
                time = 0.5
                break
            else:
                print("Invalid input. Please enter '1' or 'half'.")

        while True:
            time = int(input("Enter the time you want to hire the boat (between 10 and 17 hours): "))
            if 10 <= time <= 17:
                total_time_raw += time
                total_time_adjusted += min(time, 2)
                break
            else:
                print("Invalid time. Please enter a time between 10 and 17 hours.")

        cost = 20 if time == 1 else 12
        total_amount += cost
        boats_hired += 1
        boat_usage[boat_number - 1] += time
        print("Boat", boat_number, "hired for", time, "hour(s) at $", cost, "per hour.")

    elif hire_boat.lower() == "no":
        break
    else:
        print("Invalid input. Please enter 'yes' or 'no'.")

if boats_hired > 0:
    print("\nSummary:")
    print("Number of boats hired:", boats_hired)
    print("Total time hired :", total_time_adjusted, "hours")
    print("Total amount: $", total_amount)

    most_used_boat = boat_usage.index(max(boat_usage)) + 1
    print("Most used boat: Boat", most_used_boat)
else:
    print("No boats were hired.")
