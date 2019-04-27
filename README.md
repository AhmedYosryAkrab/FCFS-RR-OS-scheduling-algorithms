#include<iostream> 
using namespace std; 

//FCFS
  
// Function to find the waiting time for all  
// processes 
void findWaitingTime(int processes[], int n,  
                          int bt[], int wt[]) 
{ 
    // waiting time for first process is 0 
    wt[0] = 0; 
  
    // calculating waiting time 
    for (int  i = 1; i < n ; i++ ) 
        wt[i] =  bt[i-1] + wt[i-1] ; 
} 
  
// Function to calculate turn around time 
void findTurnAroundTime( int processes[], int n,  
                  int bt[], int wt[], int tat[]) 
{ 
    // calculating turnaround time by adding 
    // bt[i] + wt[i] 
    for (int  i = 0; i < n ; i++) 
        tat[i] = bt[i] + wt[i]; 
} 
  
//Function to calculate average time 
void findavgTime( int processes[], int n, int bt[]) 
{ 
    int wt[n], tat[n], total_wt = 0, total_tat = 0; 
  
    //Function to find waiting time of all processes 
    findWaitingTime(processes, n, bt, wt); 
  
    //Function to find turn around time for all processes 
    findTurnAroundTime(processes, n, bt, wt, tat); 
  
    //Display processes along with all details 
    cout << "Processes  "<< " Burst time  "
         << " Waiting time  " << " Turn around time\n"; 
  
    // Calculate total waiting time and total turn  
    // around time 
    for (int  i=0; i<n; i++) 
    { 
        total_wt = total_wt + wt[i]; 
        total_tat = total_tat + tat[i]; 
        cout << "   " << i+1 << "\t\t" << bt[i] <<"\t    "
            << wt[i] <<"\t\t  " << tat[i] <<endl; 
    } 
  
    cout << "Average waiting time = " 
         << (float)total_wt / (float)n; 
    cout << "\nAverage turn around time = " 
         << (float)total_tat / (float)n; 
} 

//RR

// Function to find the waiting time for all 
// processes 
void findWaitingTime(int processes[], int n, 
             int bt[], int wt[], int quantum) 
{ 
    // Make a copy of burst times bt[] to store remaining 
    // burst times. 
    int rem_bt[n]; 
    for (int i = 0 ; i < n ; i++) 
        rem_bt[i] =  bt[i]; 
  
    int t = 0; // Current time 
  
    // Keep traversing processes in round robin manner 
    // until all of them are not done. 
    while (1) 
    { 
        bool done = true; 
  
        // Traverse all processes one by one repeatedly 
        for (int i = 0 ; i < n; i++) 
        { 
            // If burst time of a process is greater than 0 
            // then only need to process further 
            if (rem_bt[i] > 0) 
            { 
                done = false; // There is a pending process 
  
                if (rem_bt[i] > quantum) 
                { 
                    // Increase the value of t i.e. shows 
                    // how much time a process has been processed 
                    t += quantum; 
  
                    // Decrease the burst_time of current process 
                    // by quantum 
                    rem_bt[i] -= quantum; 
                } 
  
                // If burst time is smaller than or equal to 
                // quantum. Last cycle for this process 
                else
                { 
                    // Increase the value of t i.e. shows 
                    // how much time a process has been processed 
                    t = t + rem_bt[i]; 
  
                    // Waiting time is current time minus time 
                    // used by this process 
                    wt[i] = t - bt[i]; 
  
                    // As the process gets fully executed 
                    // make its remaining burst time = 0 
                    rem_bt[i] = 0; 
                } 
            } 
        } 
  
        // If all processes are done 
        if (done == true) 
          break; 
    } 
} 
  
/* Function to calculate turn around time 
void findTurnAroundTime(int processes[], int n, 
                        int bt[], int wt[], int tat[]) 
{ 
     calculating turnaround time by adding 
     bt[i] + wt[i] 
    for (int i = 0; i < n ; i++) 
        tat[i] = bt[i] + wt[i]; 
} */
  
// Function to calculate average time 
void findavgTime(int processes[], int n, int bt[], 
                                     int quantum) 
{ 
    int wt[n], tat[n], total_wt = 0, total_tat = 0; 
  
    // Function to find waiting time of all processes 
    findWaitingTime(processes, n, bt, wt, quantum); 
  
    // Function to find turn around time for all processes 
    findTurnAroundTime(processes, n, bt, wt, tat); 
  
    // Display processes along detailed 
    cout << "Processes "<< " Burst time "
         << " Waiting time " << " Turn around time\n"; 
  
    // Calculate total waiting time and total turn 
    // around time 
    for (int i=0; i<n; i++) 
    { 
        total_wt = total_wt + wt[i]; 
        total_tat = total_tat + tat[i]; 
        cout << " " << i+1 << "\t\t" << bt[i] <<"\t "
             << wt[i] <<"\t\t " << tat[i] <<endl; 
    } 
  
    cout << "Average waiting time = "
         << (float)total_wt / (float)n; 
    cout << "\nAverage turn around time = "
         << (float)total_tat / (float)n; 
} 
  
int main() 
{ 
int a1;
int q;

cout<<"determine the number of proccesses: "<<endl;
cin>>a1;
int processes[a1] = {};
    //process id's
	 cout<<"inserts your proccesses: "<<endl;
    for(int i=0;i<a1;i++){
    	cin>>processes[i];
	}
	
	cout<<"insert quantum given: "<<endl;
	cin>>q;
    int n = sizeof processes / sizeof processes[a1]; 
  
    //Burst time of all processes 
    
     cout<<"Enter the proccess brust time to calculate FCFS and Round Robin:"<<endl;
    
    int  burst_time[a1] = {};
	  for(int j=0;j<a1;j++){
    	cin>>burst_time[j];
	}
  
  cout<<"FCFS: "<<endl;
  
    findavgTime(processes, n,  burst_time); 
    
    //
    cout<<endl;
    cout<<"RR: "<<endl;
    // Time quantum 
    int quantum = q; 
    findavgTime(processes, n, burst_time, quantum); 
    
    return 0; 
} 
