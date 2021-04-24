class TimeMap {

        private Map<String, List<StringAndTime>> key2Objs;

        /**
         * Initialize your data structure here.
         */
        public TimeMap() {
            this.key2Objs = new HashMap<>();
        }

        public void set(String key, String value, int timestamp) {
            List<StringAndTime> list = key2Objs.getOrDefault(key, new ArrayList<>());
            list.add(new StringAndTime(value, timestamp));
            key2Objs.put(key, list);
        }

        public String get(String key, int timestamp) {
            if (!this.key2Objs.containsKey(key)) {
                return "";
            }
            List<StringAndTime> list = this.key2Objs.get(key);
            int l = 0, r = list.size() - 1;
            while (l <= r) {
                int mid = (l + r) >> 1;
                StringAndTime obj = list.get(mid);
                if (obj.time == timestamp) {
                    return obj.val;
                } else if (obj.time < timestamp) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
            
            if (r < 0) return "";
            if (l > list.size() - 1) return list.get(list.size() - 1).val;
            return list.get(r).val;
        }

        class StringAndTime {
            public String val;
            public long time;
            public StringAndTime(String val, long time) {
                this.val = val;
                this.time = time;
            }
        }
}