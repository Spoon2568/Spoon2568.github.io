# Spoon2568.github.io
``C++
vector<Position> findShortestPathUsingDijkstra(const Position& start, const Position& end, int currentPlayer){
    vector<vector<int>> distances(SIZE, vector<int>(SIZE, INFINITY));
    set<Position> visited;
    vector<vector<Position>> lastNode(SIZE, vector<Position>(SIZE, inValidPosition));
    Position endLastNode = inValidPosition;
    priority_queue<Node, vector<Node>, CompareNode> pq;
    pq.push(Node(start, 0));
    //visited.insert(start);
    //distances[start.first][start.second] = 0;
    while(!pq.empty()){
        Node current = pq.top();
        pq.pop();
        if (visited.find(current.pos) != visited.end())
            continue;
        visited.insert(current.pos);


        for (auto& p:getNeighborPositions(current.pos)){
            if (visited.find(p) != visited.end())
                continue;
            if (p == end){
                endLastNode = current.pos;
                break;
            }
            else if (isInBoard(p) && (board[p.first][p.second] == 0 || board[p.first][p.second] == currentPlayer)){
                int newDistance = (board[p.first][p.second] == 0)?current.distance + 1:current.distance;
                if (newDistance < distances[p.first][p.second]){
                    distances[p.first][p.second] = newDistance;
                    pq.push(Node(p, newDistance));
                    lastNode[p.first][p.second] = current.pos;
                }
            }
        }
    }
        //cout << endl << distances[1][2] << ' ' << distances[2][5] << ' ' << distances[2][10]<< endl;
        //cout << endLastNode.first << endLastNode.second << endl;
        cout << endl << distances[10][5] << endl << endl;
        if (endLastNode == inValidPosition) return vector<Position>();
        vector<Position> path;
        Position currentPos = endLastNode;
        while (currentPos != start){
            path.push_back(currentPos);
            currentPos = lastNode[currentPos.first][currentPos.second];
        }
        reverse(path.begin(), path.end());
        return path;
}
``
