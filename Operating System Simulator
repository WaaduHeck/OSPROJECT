// ======================
// OS Project Simulator
// ======================
#include <iostream>
#include <algorithm>
#include <vector>
#include <queue>
using namespace std;

// Function declarations
void cpuSchedulingMenu();
void fcfs();
void sjf();
void roundRobin();
void priorityScheduling();
void deadlockHandlingMenu();
void bankersAlgorithm();
void memoryManagementMenu();
void pagingSimulation();
void ipcSimulationMenu();
void logicalIPC();

int main() {
    int choice;
    do {
        cout << "\n===== Operating System Simulator =====\n";
        cout << "1. CPU Scheduling Algorithms\n";
        cout << "2. Deadlock Detection & Avoidance\n";
        cout << "3. Memory Management (Paging)\n";
        cout << "4. Inter-Process Communication (Logical)\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1: cpuSchedulingMenu(); break;
            case 2: deadlockHandlingMenu(); break;
            case 3: memoryManagementMenu(); break;
            case 4: ipcSimulationMenu(); break;
            case 5: cout << "Exiting simulation... Goodbye!\n"; break;
            default: cout << "Invalid choice. Please try again.\n";
        }
    } while(choice != 5);
    return 0;
}

// CPU Scheduling Module
void cpuSchedulingMenu() {
    int option;
    do {
        cout << "\n--- CPU Scheduling Algorithms ---\n";
        cout << "1. FCFS\n2. SJF\n3. Round Robin\n4. Priority Scheduling\n5. Back\n";
        cout << "Choose: "; cin >> option;
        switch(option) {
            case 1: fcfs(); break;
            case 2: sjf(); break;
            case 3: roundRobin(); break;
            case 4: priorityScheduling(); break;
            case 5: return;
            default: cout << "Invalid option.\n";
        }
    } while(option != 5);
}

void fcfs() {
    int n; cout << "\nEnter number of processes: "; cin >> n;
    int bt[n], wt[n], tat[n];
    cout << "Enter burst times:\n";
    for(int i=0; i<n; i++) {
        cout << "P" << i+1 << ": "; cin >> bt[i];
    }
    wt[0] = 0;
    for(int i=1; i<n; i++) wt[i] = wt[i-1] + bt[i-1];
    for(int i=0; i<n; i++) tat[i] = wt[i] + bt[i];
    float totalW = 0, totalT = 0;
    cout << "\nProcess\tBurst\tWaiting\tTurnaround\n";
    for(int i=0; i<n; i++) {
        cout << "P" << i+1 << "\t" << bt[i] << "\t" << wt[i] << "\t" << tat[i] << "\n";
        totalW += wt[i]; totalT += tat[i];
    }
    cout << "Average Waiting Time: " << totalW/n << "\n";
    cout << "Average Turnaround Time: " << totalT/n << "\n";
}

void sjf() {
    int n; cout << "\nEnter number of processes: "; cin >> n;
    vector<pair<int, int>> p(n);
    for(int i=0; i<n; i++) {
        cout << "P" << i+1 << " Burst Time: ";
        cin >> p[i].first;
        p[i].second = i+1;
    }
    sort(p.begin(), p.end());
    int wt[n], tat[n]; wt[0] = 0;
    for(int i=1; i<n; i++) wt[i] = wt[i-1] + p[i-1].first;
    for(int i=0; i<n; i++) tat[i] = wt[i] + p[i].first;
    float totalW = 0, totalT = 0;
    cout << "\nProcess\tBurst\tWaiting\tTurnaround\n";
    for(int i=0; i<n; i++) {
        cout << "P" << p[i].second << "\t" << p[i].first << "\t" << wt[i] << "\t" << tat[i] << "\n";
        totalW += wt[i]; totalT += tat[i];
    }
    cout << "Average Waiting Time: " << totalW/n << "\n";
    cout << "Average Turnaround Time: " << totalT/n << "\n";
}

void roundRobin() {
    int n, q;
    cout << "\nEnter number of processes: "; cin >> n;
    cout << "Enter time quantum: "; cin >> q;
    int bt[n], rt[n], wt[n] = {}, tat[n];
    for(int i=0; i<n; i++) {
        cout << "P" << i+1 << " Burst Time: "; cin >> bt[i];
        rt[i] = bt[i];
    }
    int t = 0; bool done;
    do {
        done = true;
        for(int i=0; i<n; i++) {
            if(rt[i] > 0) {
                done = false;
                if(rt[i] > q) { t += q; rt[i] -= q; }
                else { t += rt[i]; wt[i] = t - bt[i]; rt[i] = 0; }
            }
        }
    } while(!done);
    for(int i=0; i<n; i++) tat[i] = bt[i] + wt[i];
    float totalW = 0, totalT = 0;
    cout << "\nProcess\tBurst\tWaiting\tTurnaround\n";
    for(int i=0; i<n; i++) {
        cout << "P" << i+1 << "\t" << bt[i] << "\t" << wt[i] << "\t" << tat[i] << "\n";
        totalW += wt[i]; totalT += tat[i];
    }
    cout << "Average Waiting Time: " << totalW/n << "\n";
    cout << "Average Turnaround Time: " << totalT/n << "\n";
}

void priorityScheduling() {
    int n; cout << "\nEnter number of processes: "; cin >> n;
    int bt[n], p[n], idx[n], wt[n], tat[n];
    for(int i=0; i<n; i++) {
        cout << "P" << i+1 << " Burst & Priority: "; cin >> bt[i] >> p[i];
        idx[i] = i+1;
    }
    for(int i=0; i<n-1; i++) {
        for(int j=i+1; j<n; j++) {
            if(p[i]>p[j]) swap(p[i],p[j]), swap(bt[i],bt[j]), swap(idx[i],idx[j]);
        }
    }
    wt[0] = 0;
    for(int i=1; i<n; i++) wt[i] = wt[i-1] + bt[i-1];
    for(int i=0; i<n; i++) tat[i] = wt[i] + bt[i];
    float totalW = 0, totalT = 0;
    cout << "\nProcess\tBurst\tPriority\tWaiting\tTurnaround\n";
    for(int i=0; i<n; i++) {
        cout << "P" << idx[i] << "\t" << bt[i] << "\t" << p[i] << "\t\t" << wt[i] << "\t" << tat[i] << "\n";
        totalW += wt[i]; totalT += tat[i];
    }
    cout << "Average Waiting Time: " << totalW/n << "\n";
    cout << "Average Turnaround Time: " << totalT/n << "\n";
}

// Deadlock Handling
void deadlockHandlingMenu() {
    cout << "\n--- Deadlock Avoidance using Banker's Algorithm ---\n";
    bankersAlgorithm();
}

void bankersAlgorithm() {
    int n, m;
    cout << "Enter number of processes: "; cin >> n;
    cout << "Enter number of resources: "; cin >> m;

    int alloc[n][m], max[n][m], avail[m], need[n][m];
    cout << "Enter allocation matrix:\n";
    for(int i=0;i<n;i++) for(int j=0;j<m;j++) cin >> alloc[i][j];

    cout << "Enter maximum matrix:\n";
    for(int i=0;i<n;i++) for(int j=0;j<m;j++) cin >> max[i][j];

    cout << "Enter available resources:\n";
    for(int j=0;j<m;j++) cin >> avail[j];

    for(int i=0;i<n;i++) for(int j=0;j<m;j++) need[i][j] = max[i][j] - alloc[i][j];

    bool finish[n] = {}; vector<int> safeSeq;
    while(safeSeq.size() < n) {
        bool found = false;
        for(int i=0;i<n;i++) {
            if(!finish[i]) {
                bool canRun = true;
                for(int j=0;j<m;j++) if(need[i][j] > avail[j]) canRun = false;
                if(canRun) {
                    for(int j=0;j<m;j++) avail[j] += alloc[i][j];
                    finish[i] = true; found = true;
                    safeSeq.push_back(i);
                }
            }
        }
        if(!found) break;
    }
    if(safeSeq.size() == n) {
        cout << "Safe Sequence: ";
        for(int i : safeSeq) cout << "P" << i << " ";
        cout << "\nSystem is in a safe state.\n";
    } else {
        cout << "System is in DEADLOCK.\n";
    }
}

// Memory Management
void memoryManagementMenu() {
    cout << "\n--- Memory Management using Paging ---\n";
    pagingSimulation();
}

void pagingSimulation() {
    int memSize, pageSize;
    cout << "Enter memory size: "; cin >> memSize;
    cout << "Enter page size: "; cin >> pageSize;
    int numPages = memSize / pageSize;
    cout << "Total number of pages: " << numPages << "\n";
    cout << "Enter number of processes: ";
    int n; cin >> n;
    for(int i=0; i<n; i++) {
        int processSize;
        cout << "Process " << i+1 << " size: "; cin >> processSize;
        int pagesNeeded = (processSize + pageSize - 1) / pageSize;
        if(pagesNeeded > numPages) {
            cout << "Not enough memory for process " << i+1 << "\n";
        } else {
            cout << "Process " << i+1 << " requires " << pagesNeeded << " pages.\n";
            numPages -= pagesNeeded;
        }
    }
}

// IPC Simulation
void ipcSimulationMenu() {
    cout << "\n--- Logical Inter-Process Communication ---\n";
    logicalIPC();
}

void logicalIPC() {
    queue<string> messageQueue;
    string msg; char option;
    do {
        cout << "Send a message: ";
        cin.ignore(); getline(cin, msg);
        messageQueue.push(msg);
        cout << "Send another message? (y/n): ";
        cin >> option;
    } while(option == 'y');

    cout << "\nMessages received:\n";
    while(!messageQueue.empty()) {
        cout << "-> " << messageQueue.front() << "\n";
        messageQueue.pop();
    }
}
