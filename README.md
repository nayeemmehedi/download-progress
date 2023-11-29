## download-progress

 // FetchComponent.js
    
    import React, { useState } from 'react';
    import axios from 'axios';
    
    const FetchComponent = () => {
      const [loading, setLoading] = useState(false);
      const [progress, setProgress] = useState(0);
    
      const fetchData = async () => {
        try {
          setLoading(true);
    
          const response = await axios.get('https://api.example.com/data', {
            onDownloadProgress: (progressEvent) => {
              const percentCompleted = Math.round(
                (progressEvent.loaded * 100) / progressEvent.total
              );
              setProgress(percentCompleted);
            },
          });
    
          // Handle the response as needed
          console.log(response.data);
        } catch (error) {
          // Handle errors
          console.error(error);
        } finally {
          setLoading(false);
        }
      };
    
      return (
        <div>
          {loading && <p>Loading: {progress}%</p>}
          <button onClick={fetchData} disabled={loading}>
            {loading ? 'Fetching...' : 'Fetch Data'}
          </button>
        </div>
      );
    };
    
    export default FetchComponent;
