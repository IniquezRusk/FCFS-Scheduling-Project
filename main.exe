#include <iostream>
#include <iomanip>
using namespace std;

const int MAXP = 50;

struct Process {
    int pid;
    int arrival;
    int burst;

    int start;
    int finish;
    int waiting;
    int turnaround;
};

void printMenu() {
    cout << "FCFS CPU Scheduling" << endl;
    cout << "1. Enter the processes manually\n";
    cout << "2. Use sample test case\n";
    cout << "3. Exit\n";
    cout << "Choose an option: ";
}

void inputProcesses(Process p[], int &n) {
    cout << "How many processes (1-" << MAXP << ")? ";
    cin >> n;
    if (n < 1) n = 1;
    if (n > MAXP) n = MAXP;

    cout << "\nEnter arrival time and burst time for each process:\n";
    for (int i = 0; i < n; i++) {
        p[i].pid = i + 1;
        cout << "P" << p[i].pid << " arrival time: ";
        cin >> p[i].arrival;
        cout << "P" << p[i].pid << " burst time: ";
        cin >> p[i].burst;
    }
}

void loadSample(Process p[], int &n) {
    // Test case
    n = 4;
    p[0] = {1, 0, 5, 0, 0, 0, 0};
    p[1] = {2, 2, 3, 0, 0, 0, 0};
    p[2] = {3, 4, 1, 0, 0, 0, 0};
    p[3] = {4, 6, 2, 0, 0, 0, 0};

    cout << "\nUsing sample test case (PID, arrival, burst):\n";
    for (int i = 0; i < n; i++) {
        cout << "P" << p[i].pid
             << " -> A=" << p[i].arrival
             << ", B=" << p[i].burst << "\n";
    }
}

void sortByArrival(Process p[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (p[j].arrival < p[i].arrival) {
                Process temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }
}

void runFCFS(Process p[], int n) {
    sortByArrival(p, n);

    int current_time = 0;
    double total_wait = 0.0;
    double total_turn = 0.0;
    double max_turn   = 0.0;

    cout << "\n--- Step-by-step CPU timeline ---\n";

    for (int i = 0; i < n; i++) {
        // CPU stays idle until this process arrives
        while (current_time < p[i].arrival) {
            cout << "Time " << current_time << ": CPU idle\n";
            current_time++;
        }

        // Start the process
        p[i].start = current_time;
        cout << "Process P" << p[i].pid
             << " starts at time " << p[i].start << '\n';

        // Run for its burst time
        for (int t = 0; t < p[i].burst; t++) {
            cout << "Time " << current_time
                 << ": running P" << p[i].pid << '\n';
            current_time++;
        }

        // Finish and metrics
        p[i].finish     = current_time;
        p[i].waiting    = p[i].start - p[i].arrival;
        p[i].turnaround = p[i].finish - p[i].arrival;

        total_wait += p[i].waiting;
        total_turn += p[i].turnaround;

        if (p[i].turnaround > max_turn) {
            max_turn = p[i].turnaround;
        }

        cout << "Process P" << p[i].pid
             << " finished at time " << p[i].finish << "\n\n";
    }

    // Results table (once, after all processes)
    cout << "\n--- Results table ---\n";
    cout << setw(5)  << "PID"
         << setw(10) << "Arrive"
         << setw(8)  << "Burst"
         << setw(8)  << "Start"
         << setw(8)  << "Finish"
         << setw(10) << "Waiting"
         << setw(12) << "Turnaround" << '\n';

    for (int i = 0; i < n; ++i) {
        cout << setw(5)  << p[i].pid
             << setw(10) << p[i].arrival
             << setw(8)  << p[i].burst
             << setw(8)  << p[i].start
             << setw(8)  << p[i].finish
             << setw(10) << p[i].waiting
             << setw(12) << p[i].turnaround
             << '\n';
    }

    cout.setf(ios::fixed);
    cout.precision(2);
    cout << "\nAverage waiting time    = "
         << (total_wait / n) << '\n';
    cout << "Average turnaround time = "
         << (total_turn / n) << '\n';
    cout << "Max turnaround time     = "
         << max_turn << "\n";
}

int main() {
    Process procs[MAXP];
    int n;
    int choice;

    while (true) {
        printMenu();
        cin >> choice;

        if (choice == 3) {
            cout << "Exiting...\n";
            break;
        } else if (choice == 1) {
            inputProcesses(procs, n);
        } else if (choice == 2) {
            loadSample(procs, n);
        } else {
            cout << "Invalid option.\n";
            continue;
        }

        runFCFS(procs, n);
    }

    return 0;
}
