# wavenlabs
Assignment


public class Distance {

	public int networkDelayTime(int[][] times, int n, int k) {
		int[][] graph = new int[n+1][n+1];
		for (int[] time : times) {
			graph[time[0]][time[1]] = time[2];
		}

		boolean[] visited = new boolean[n+1];
		int[] dist = new int[n+1];
		Arrays.fill(dist, Integer.MAX_VALUE);
		dist[k] = 0;

		for (int i = 1; i < n; i++) {
			int u = -1;
			for (int j = 1; j <= n; j++) {
				if (!visited[j] && (u == -1 || dist[j] < dist[u])) {
					u = j;
				}
			}
			visited[u] = true;
			for (int v = 1; v <= n; v++) {
				if (graph[u][v] != 0) {
					int newDist = dist[u] + graph[u][v];
					if (newDist < dist[v]) {
						dist[v] = newDist;
					}
				}
			}
		}

		int maxDist = 0;
		for (int i = 1; i <= n; i++) {
			if (dist[i] == Integer.MAX_VALUE) {
				return -1;
			}
			maxDist = Math.max(maxDist, dist[i]);
		}
		return maxDist;
	}
	public static void main(String[] args) {
		int[][] times={{2,1,1},{2,3,1},{3,4,1}};
		int n=4;
		int k=2;
		Distance d=new Distance();
		System.out.println(d.networkDelayTime(times, n, k));
	}
}
