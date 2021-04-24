class TopVotedCandidate {

        private int[] times;
        private int[] winners;

        public TopVotedCandidate(int[] persons, int[] times) {
            this.times = times;
            this.winners = new int[times.length];
            Map<Integer, Integer> person2VoteCnt = new HashMap<>();
            int preWinner = persons[0], curHighestVoteCnt = 1;
            person2VoteCnt.put(preWinner, 1);
            winners[0] = preWinner;
            for (int i = 1; i < persons.length; i ++) {
                int thisPerson = persons[i];
                int thisPersonVoteCnt = person2VoteCnt.getOrDefault(thisPerson, 0) + 1;
                person2VoteCnt.put(thisPerson, thisPersonVoteCnt);
                if (thisPerson == preWinner) {
                    winners[i] = preWinner;
                    curHighestVoteCnt = thisPersonVoteCnt;
                    continue;
                }
                if (thisPersonVoteCnt < curHighestVoteCnt) {
                    winners[i] = preWinner;
                } else {
                    winners[i] = thisPerson;
                    preWinner = thisPerson;
                    curHighestVoteCnt = thisPersonVoteCnt;
                }
            }
        }

        public int q(int t) {
            int l = 0, r = times.length - 1;
            while (l <= r) {
                int mid = (l + r) >> 1;
                int time = times[mid];
                if (time == t) return winners[mid];
                if (t > time) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
            return l > winners.length - 1 ? winners[winners.length - 1] : winners[r];
        }
}