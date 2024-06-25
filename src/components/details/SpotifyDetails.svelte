<script lang="ts">
  const clientid = "414a39833d0a463094a69cf1f04d289c";
  const clientsecret = "16519f4fb65e46629096ad92ef42e94c";
  
  const GetAccessKey = async (): Promise<string> => {
    const result = await fetch("https://accounts.spotify.com/api/token", {
      method: "POST",
      headers: {
        "Content-Type" : "application/x-www-form-urlencoded",
        "Authorization" : "Basic " + btoa(clientid + ":" + clientsecret),
      },
      body: "grant_type=client_credentials"
    });
    
    const data = await result.json();
    return data.access_token;
  };

  const GetTopArtist = async (token: string) => {
    const result = await fetch("https://api.spotify.com/v1/me/top/artists?offset=0&time_range=short_term&locale=en-US,en;q%3D0.5", {
        method: "GET",
        headers: {
            "Authorization": "Bearer " + token
        }
    });

    const data = await result.json();
    return data;
  };

  GetAccessKey().then(token => {
    GetTopArtist(token).then(artists => {
      console.log(artists);
    });
  });
</script>
