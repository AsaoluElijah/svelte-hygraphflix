<script>
  import { ApolloClient, InMemoryCache } from "@apollo/client/core";
  import { setClient } from "svelte-apollo";
  import Movies from "./Movies.svelte";

  const client = new ApolloClient({
    uri: "https://api-us-east-1-shared-usea1-02.hygraph.com/v2/cluh3nib3000008jk3ippd87t/master",
    cache: new InMemoryCache(),
  });
  setClient(client);
</script>

<Movies />
