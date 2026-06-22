# CIS567-integrated-lab-3
CIS 567 third Integrated Lab - Credit card debt proram (zyBooks 26.22)


```python
def read_customer_data(filename):
    """Read and return data from filename as a list of lists (name, state, debt)"""
    names = []
    states = []
    debts = []

    with open(filename) as f:
        rows = f.readlines()
    for row in rows:
        row = row.split(",")
        names.append(row[0])
        states.append(row[1])
        debts.append(float(row[2].strip()))
    return names, states, debts


# Main portion of the program
if __name__ == "__main__":
    # number of rows to consider
    num_customers = int(input())

    names, states, debts = read_customer_data("CustomerData.csv")

    # Type your code here.
    debt_limit = int(input())
    search_phrase = input()
    state_abbr = input()

    print("U.S. Report")
    print("Customers:", num_customers)

    highest_name = names[0]
    highest_debt = debts[0]
    for i in range(num_customers):
        if debts[i] > highest_debt:
            highest_debt = debts[i]
            highest_name = names[i]
    print("Highest debt:", highest_name)

    start_count = 0
    for i in range(num_customers):
        if names[i].startswith(search_phrase):
            start_count += 1
    print('Customer names that start with "' + search_phrase + '":', start_count)

    over_count = 0
    free_count = 0
    for i in range(num_customers):
        if debts[i] > debt_limit:
            over_count += 1
        if debts[i] == 0:
            free_count += 1
    print("Customers with debt over $" + str(debt_limit) + ":", over_count)
    print("Customers debt free:", free_count)

    print()
    print(state_abbr + " Report")

    state_total = 0
    for i in range(num_customers):
        if states[i].strip() == state_abbr:
            state_total += 1
    print("Customers:", state_total)

    state_high_name = ""
    state_high_debt = -1.0
    for i in range(num_customers):
        if states[i].strip() == state_abbr:
            if debts[i] > state_high_debt:
                state_high_debt = debts[i]
                state_high_name = names[i]
    print("Highest debt:", state_high_name)

    state_start = 0
    for i in range(num_customers):
        if states[i].strip() == state_abbr and names[i].startswith(search_phrase):
            state_start += 1
    print('Customer names that start with "' + search_phrase + '":', state_start)

    state_over = 0
    state_free = 0
    for i in range(num_customers):
        if states[i].strip() == state_abbr:
            if debts[i] > debt_limit:
                state_over += 1
            if debts[i] == 0:
                state_free += 1
    print("Customers with debt over $" + str(debt_limit) + ":", state_over)
    print("Customers debt free:", state_free)
```
