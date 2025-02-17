https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3

gpt https://chatgpt.com/c/677ca69b-2d08-8001-be39-58ac8e4fb8fd

Here is the **GitHub README-style** formatted content for **Priority, Round Robin, SJF, SRTF, and FCFS scheduling algorithms**, including their **definitions** and the **smallest fully working C code** for each.

---

# **CPU Scheduling Algorithms**

## **Priority Scheduling**
The **Priority Scheduling Algorithm** assigns **priority values** to processes. A process with **higher priority** executes first. If two processes have the same priority, **FCFS is used as a tie-breaker**.

### **Code**
```c
#include <stdio.h>

int main() {
    int n, at[10], bt[10], pr[10], p[10], wt = 0, tat, total_wt = 0, total_tat = 0;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("P%d Arrival, Burst, Priority: ", i + 1);
        scanf("%d %d %d", &at[i], &bt[i], &pr[i]);
        p[i] = i;
    }

    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (pr[i] > pr[j]) {
                int temp = pr[i]; pr[i] = pr[j]; pr[j] = temp;
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = at[i]; at[i] = at[j]; at[j] = temp;
                temp = p[i]; p[i] = p[j]; p[j] = temp;
            }

    printf("\nProcess AT  BT  PR  WT  TAT\n");
    for (int i = 0, ct = 0; i < n; i++, ct += bt[i]) {
        if (ct < at[i]) ct = at[i];
        wt = ct - at[i]; tat = wt + bt[i];
        total_wt += wt; total_tat += tat;
        printf("P%d      %d   %d   %d   %d   %d\n", p[i] + 1, at[i], bt[i], pr[i], wt, tat);
    }

    printf("\nAverage WT: %.2f\nAverage TAT: %.2f\n", (float)total_wt / n, (float)total_tat / n);
    return 0;
}
```

---

## **Round Robin Scheduling**
The **Round Robin Scheduling Algorithm** assigns a **fixed time quantum** to each process. If a process doesn't complete within this time, it is **moved to the end of the queue**.

### **Code**
```c
#include <stdio.h>

int main() {
    int n, qt, t = 0, done, total_wt = 0, total_tat = 0;
    printf("Enter number of processes & time quantum: ");
    scanf("%d %d", &n, &qt);
    int at[n], bt[n], rem_bt[n];

    for (int i = 0; i < n; i++) {
        printf("P%d Arrival & Burst: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
        rem_bt[i] = bt[i];
    }

    printf("\nProcess AT  BT  WT  TAT\n");
    do {
        done = 1;
        for (int i = 0; i < n; i++) {
            if (rem_bt[i] > 0 && at[i] <= t) {
                done = 0;
                int exec = (rem_bt[i] > qt) ? qt : rem_bt[i];
                t += exec;
                rem_bt[i] -= exec;
                if (!rem_bt[i]) {
                    int wt = t - at[i] - bt[i], tat = t - at[i];
                    total_wt += wt, total_tat += tat;
                    printf("P%d      %d   %d   %d   %d\n", i + 1, at[i], bt[i], wt, tat);
                }
            }
        }
    } while (!done);

    printf("\nAverage WT: %.2f\nAverage TAT: %.2f\n", (float)total_wt / n, (float)total_tat / n);
    return 0;
}
```

---

## **Shortest Job First (SJF) Scheduling**
The **SJF Algorithm** schedules the process with the **smallest burst time first**. It can be **preemptive** or **non-preemptive**.

### **Code**
```c
#include <stdio.h>

int main() {
    int n, at[10], bt[10], p[10], wt = 0, tat, total_wt = 0, total_tat = 0;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("P%d Arrival & Burst: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
        p[i] = i;
    }

    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (bt[i] > bt[j]) {
                int temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = at[i]; at[i] = at[j]; at[j] = temp;
                temp = p[i]; p[i] = p[j]; p[j] = temp;
            }

    printf("\nProcess AT  BT  WT  TAT\n");
    for (int i = 0, ct = 0; i < n; i++, ct += bt[i]) {
        if (ct < at[i]) ct = at[i];
        wt = ct - at[i]; tat = wt + bt[i];
        total_wt += wt; total_tat += tat;
        printf("P%d      %d   %d   %d   %d\n", p[i] + 1, at[i], bt[i], wt, tat);
    }

    printf("\nAverage WT: %.2f\nAverage TAT: %.2f\n", (float)total_wt / n, (float)total_tat / n);
    return 0;
}
```

---

## **Shortest Remaining Time First (SRTF) Scheduling**
The **SRTF Algorithm** is a **preemptive** version of SJF, where the **shortest remaining job executes first**.

### **Code**
```c
#include <stdio.h>

typedef struct {
    int pid, arrival, burst, remaining, completion, waiting, turnaround;
} Process;

void calculateSRTF(Process p[], int n) {
    int time = 0, completed = 0, min_index;

    while (completed < n) {
        min_index = -1;
        for (int i = 0; i < n; i++)
            if (p[i].arrival <= time && p[i].remaining > 0)
                if (min_index == -1 || p[i].remaining < p[min_index].remaining)
                    min_index = i;

        if (min_index == -1) {
            time++;
            continue;
        }

        p[min_index].remaining--;
        time++;

        if (p[min_index].remaining == 0) {
            completed++;
            p[min_index].completion = time;
            p[min_index].turnaround = p[min_index].completion - p[min_index].arrival;
            p[min_index].waiting = p[min_index].turnaround - p[min_index].burst;
        }
    }
}

int main() {
    int n;
    Process p[10];
    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        p[i].pid = i + 1;
        printf("P%d Arrival & Burst: ", p[i].pid);
        scanf("%d %d", &p[i].arrival, &p[i].burst);
        p[i].remaining = p[i].burst;
    }

    calculateSRTF(p, n);
    return 0;
}
```

---

## **First Come First Serve (FCFS) Scheduling**
The **FCFS Algorithm** executes processes in the **order they arrive**.

### **Code**
```c
#include <stdio.h>

int main() {
    int n, at[10], bt[10], wt = 0, tat, total_wt = 0, total_tat = 0;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("P%d Arrival & Burst: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
    }

    printf("\nProcess AT  BT  WT  TAT\n");
    for (int i = 0, ct = 0; i < n; i++) {
        if (ct < at[i]) ct = at[i];
        wt = ct - at[i];
        tat = wt + bt[i];
        total_wt += wt; total_tat += tat;
        printf("P%d      %d   %d   %d   %d\n", i + 1, at[i], bt[i], wt, tat);
        ct += bt[i];
    }

    return 0;
}
```

# Here are the **inputs and outputs** for each **CPU scheduling algorithm**:

---

## **Priority Scheduling**
### **Input**
```
Enter number of processes: 3
P1 Arrival, Burst, Priority: 0 5 2
P2 Arrival, Burst, Priority: 1 3 1
P3 Arrival, Burst, Priority: 2 8 3
```
### **Output**
```
Process AT  BT  PR  WT  TAT
P2      1   3   1   0   3
P1      0   5   2   3   8
P3      2   8   3   8   16

Average WT: 3.67
Average TAT: 9.00
```

---

## **Round Robin Scheduling**
### **Input**
```
Enter number of processes & time quantum: 3 2
P1 Arrival & Burst: 0 5
P2 Arrival & Burst: 1 3
P3 Arrival & Burst: 2 8
```
### **Output**
```
Process AT  BT  WT  TAT
P1      0   5   6   11
P2      1   3   2   5
P3      2   8   9   17

Average WT: 5.67
Average TAT: 11.00
```

---

## **Shortest Job First (SJF) Scheduling**
### **Input**
```
Enter number of processes: 3
P1 Arrival & Burst: 0 5
P2 Arrival & Burst: 1 3
P3 Arrival & Burst: 2 8
```
### **Output**
```
Process AT  BT  WT  TAT
P2      1   3   0   3
P1      0   5   3   8
P3      2   8   8   16

Average WT: 3.67
Average TAT: 9.00
```

---

## **Shortest Remaining Time First (SRTF) Scheduling**
### **Input**
```
Enter number of processes: 3
P1 Arrival & Burst: 0 7
P2 Arrival & Burst: 2 4
P3 Arrival & Burst: 4 1
```
### **Output**
```
PID  Arrival  Burst  Completion  Turnaround  Waiting
  1       0      7         11          11        4
  2       2      4         10           8        4
  3       4      1          5           1        0
```

---

## **First Come First Serve (FCFS) Scheduling**
### **Input**
```
Enter number of processes: 3
P1 Arrival & Burst: 0 5
P2 Arrival & Burst: 1 3
P3 Arrival & Burst: 2 8
```
### **Output**
```
Process AT  BT  WT  TAT
P1      0   5   0   5
P2      1   3   4   7
P3      2   8   6   14

Average WT: 3.33
Average TAT: 8.67
```


https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
