1. Input Phase

Pod with specific requirements (2GB memory, 1 CPU, SSD disk)
4 nodes with different capabilities and states

2. PreFilter Phase

Global validation step before node-by-node filtering
Checks cluster-wide constraints and can abort early

3. Filter Phase (Sequential Elimination)

NodeResourcesFit: Eliminates Node-2 (insufficient memory)
NodeAffinity: Checks remaining nodes for SSD requirement
NodeUnschedulable: Eliminates Node-4 (marked unschedulable)
Result: Only Node-1 and Node-3 remain feasible

4. PostFilter Phase (Preemption)

Only triggers when no feasible nodes found
Last resort attempt to evict lower-priority pods
Either succeeds and continues, or fails and marks pod unschedulable

5. Score Phase (Ranking Competition)

NodeResourcesFit: Node-3 scores higher (75% vs 50% free resources)
NodeAffinity: Both score perfectly (100) for SSD match
Additional plugins: Volume, topology favor Node-3
Weighted combination: Produces final scores

6. Winner Selection

Node-3 wins with 265 points vs Node-1's 230 points
Best overall fit: Superior resource availability + perfect requirements match
Continues to binding cycle