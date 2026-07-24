1. The most painful part of building this without a framework is handling POST requests and manually parsing the body data.
2. We have to manually collect these chunks and combine them into a single string so we can parse the complete JSON object once the stream finishes (req.on('end')).
3. The 201 Created status code. Why? It is specifically used for POST requests to explicitly tell the client: "I received your request, it was successful, and a new resource was created on the server as a result."
4. DELETE /api/tasks?task=Learn Node.js):
//ROUTE 5: DELETE /api/tasks
if (pathname === '/api/tasks' && method === 'DELETE') {
    
    const taskToDelete = parsedUrl.searchParams.get('task');
    const taskIndex = tasks.indexOf(taskToDelete);

    if (taskIndex !== -1) {
        // 3a. If it exists, remove it from the array
        tasks.splice(taskIndex, 1);
        
        // Return 200 OK (Success)
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ message: `Deleted task: ${taskToDelete}` }));
    } else {
        // 3b. If it doesn't exist, return an error
        
        // Return 404 Not Found
        res.writeHead(404, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'Task not found' }));
    }
    
    return;
}
