<script lang="ts">
	var today = new Date();
	var dd = String(today.getDate()).padStart(2, '0');
	var mm = String(today.getMonth() + 1).padStart(2, '0');
	var yyyy = today.getFullYear();

	let launch_date = $state<string>(yyyy + '-' + mm + '-' + dd);

	let min_date = '2025-03-11';
	let max_date = '2025-10-28';

	let parsed_min_date = Date.parse(min_date);
	let parsed_max_date = Date.parse(max_date);

	let tides: { [id: string]: { time: string; height: string } } = {
		'2025-03-11': { time: '9:75', height: '1.37' },
		'2025-03-12': { time: '10:5', height: '1.11' },
		'2025-03-13': { time: '11:1', height: '0.95' },
		'2025-03-14': { time: '11:63', height: '0.89' },
		'2025-03-15': { time: '12:07', height: '0.91' },
		'2025-03-16': { time: '12:47', height: '0.99' },
		'2025-03-17': { time: '12:85', height: '1.1' },
		'2025-03-18': { time: '13:23', height: '1.22' },
		'2025-03-19': { time: '13:65', height: '1.37' },
		'2025-03-20': { time: '14:16', height: '1.57' },
		'2025-03-21': { time: '14:83', height: '1.82' },
		'2025-03-22': { time: '15:81', height: '2.09' },
		'2025-03-23': { time: '17:35', height: '2.27' },
		'2025-03-24': { time: '6:23', height: '2.1' },
		'2025-03-25': { time: '7:75', height: '1.84' },
		'2025-03-26': { time: '8:8', height: '1.42' },
		'2025-03-27': { time: '9:64', height: '0.98' },
		'2025-03-28': { time: '10:37', height: '0.6' },
		'2025-03-29': { time: '11:06', height: '0.33' },
		'2025-03-30': { time: '11:74', height: '0.2' },
		'2025-03-31': { time: '12:41', height: '0.24' },
		'2025-04-01': { time: '13:1', height: '0.44' },
		'2025-04-02': { time: '13:82', height: '0.77' },
		'2025-04-03': { time: '14:62', height: '1.2' },
		'2025-04-04': { time: '15:55', height: '1.65' },
		'2025-04-05': { time: '16:79', height: '2.03' },
		'2025-04-06': { time: '5:51', height: '1.91' },
		'2025-04-07': { time: '7:17', height: '1.89' },
		'2025-04-08': { time: '8:48', height: '1.65' },
		'2025-04-09': { time: '9:41', height: '1.38' },
		'2025-04-10': { time: '10:12', height: '1.18' },
		'2025-04-11': { time: '10:7', height: '1.06' },
		'2025-04-12': { time: '11:18', height: '1.03' },
		'2025-04-13': { time: '11:6', height: '1.04' },
		'2025-04-14': { time: '11:98', height: '1.09' },
		'2025-04-15': { time: '12:35', height: '1.15' },
		'2025-04-16': { time: '12:75', height: '1.23' },
		'2025-04-17': { time: '13:23', height: '1.34' },
		'2025-04-18': { time: '13:81', height: '1.5' },
		'2025-04-19': { time: '14:56', height: '1.71' },
		'2025-04-20': { time: '15:57', height: '1.94' },
		'2025-04-21': { time: '16:96', height: '2.07' },
		'2025-04-22': { time: '5:75', height: '1.95' },
		'2025-04-23': { time: '7:15', height: '1.72' },
		'2025-04-24': { time: '8:24', height: '1.36' },
		'2025-04-25': { time: '9:13', height: '0.98' },
		'2025-04-26': { time: '9:92', height: '0.66' },
		'2025-04-27': { time: '10:66', height: '0.44' },
		'2025-04-28': { time: '11:37', height: '0.35' },
		'2025-04-29': { time: '12:08', height: '0.4' },
		'2025-04-30': { time: '12:8', height: '0.59' },
		'2025-05-01': { time: '13:56', height: '0.88' },
		'2025-05-02': { time: '14:37', height: '1.24' },
		'2025-05-03': { time: '15:31', height: '1.6' },
		'2025-05-04': { time: '16:45', height: '1.9' },
		'2025-05-05': { time: '5:15', height: '1.82' },
		'2025-05-06': { time: '6:61', height: '1.85' },
		'2025-05-07': { time: '7:88', height: '1.73' },
		'2025-05-08': { time: '8:85', height: '1.56' },
		'2025-05-09': { time: '9:59', height: '1.42' },
		'2025-05-10': { time: '10:19', height: '1.33' },
		'2025-05-11': { time: '10:69', height: '1.29' },
		'2025-05-12': { time: '11:14', height: '1.27' },
		'2025-05-13': { time: '11:56', height: '1.26' },
		'2025-05-14': { time: '11:99', height: '1.26' },
		'2025-05-15': { time: '12:48', height: '1.28' },
		'2025-05-16': { time: '13:04', height: '1.33' },
		'2025-05-17': { time: '13:7', height: '1.43' },
		'2025-05-18': { time: '14:48', height: '1.57' },
		'2025-05-19': { time: '15:44', height: '1.71' },
		'2025-05-20': { time: '16:58', height: '1.81' },
		'2025-05-21': { time: '5:24', height: '1.75' },
		'2025-05-22': { time: '6:5', height: '1.64' },
		'2025-05-23': { time: '7:63', height: '1.43' },
		'2025-05-24': { time: '8:61', height: '1.17' },
		'2025-05-25': { time: '9:5', height: '0.93' },
		'2025-05-26': { time: '10:31', height: '0.76' },
		'2025-05-27': { time: '11:09', height: '0.67' },
		'2025-05-28': { time: '11:84', height: '0.68' },
		'2025-05-29': { time: '12:6', height: '0.79' },
		'2025-05-30': { time: '13:36', height: '0.97' },
		'2025-05-31': { time: '14:16', height: '1.2' },
		'2025-06-01': { time: '15:01', height: '1.46' },
		'2025-06-02': { time: '15:94', height: '1.69' },
		'2025-06-03': { time: '17:', height: '1.87' },
		'2025-06-04': { time: '5:72', height: '1.88' },
		'2025-06-05': { time: '6:93', height: '1.93' },
		'2025-06-06': { time: '8:01', height: '1.89' },
		'2025-06-07': { time: '8:89', height: '1.8' },
		'2025-06-08': { time: '9:6', height: '1.71' },
		'2025-06-09': { time: '10:2', height: '1.61' },
		'2025-06-10': { time: '10:74', height: '1.51' },
		'2025-06-11': { time: '11:25', height: '1.42' },
		'2025-06-12': { time: '11:78', height: '1.33' },
		'2025-06-13': { time: '12:35', height: '1.26' },
		'2025-06-14': { time: '12:96', height: '1.23' },
		'2025-06-15': { time: '13:63', height: '1.25' },
		'2025-06-16': { time: '14:37', height: '1.32' },
		'2025-06-17': { time: '15:2', height: '1.42' },
		'2025-06-18': { time: '16:13', height: '1.54' },
		'2025-06-19': { time: '17:18', height: '1.63' },
		'2025-06-20': { time: '5:84', height: '1.64' },
		'2025-06-21': { time: '7:02', height: '1.62' },
		'2025-06-22': { time: '8:15', height: '1.5' },
		'2025-06-23': { time: '9:18', height: '1.34' },
		'2025-06-24': { time: '10:09', height: '1.16' },
		'2025-06-25': { time: '10:93', height: '1.03' },
		'2025-06-26': { time: '11:71', height: '0.94' },
		'2025-06-27': { time: '12:45', height: '0.93' },
		'2025-06-28': { time: '13:17', height: '0.99' },
		'2025-06-29': { time: '13:87', height: '1.12' },
		'2025-06-30': { time: '14:57', height: '1.29' },
		'2025-07-01': { time: '15:29', height: '1.49' },
		'2025-07-02': { time: '16:06', height: '1.71' },
		'2025-07-03': { time: '16:94', height: '1.91' },
		'2025-07-04': { time: '5:62', height: '2.11' },
		'2025-07-05': { time: '6:79', height: '2.23' },
		'2025-07-06': { time: '7:97', height: '2.21' },
		'2025-07-07': { time: '8:96', height: '2.09' },
		'2025-07-08': { time: '9:74', height: '1.91' },
		'2025-07-09': { time: '10:4', height: '1.7' },
		'2025-07-10': { time: '11:01', height: '1.48' },
		'2025-07-11': { time: '11:59', height: '1.28' },
		'2025-07-12': { time: '12:19', height: '1.12' },
		'2025-07-13': { time: '12:8', height: '1.01' },
		'2025-07-14': { time: '13:44', height: '0.98' },
		'2025-07-15': { time: '14:11', height: '1.03' },
		'2025-07-16': { time: '14:85', height: '1.15' },
		'2025-07-17': { time: '15:66', height: '1.34' },
		'2025-07-18': { time: '16:6', height: '1.55' },
		'2025-07-19': { time: '5:24', height: '1.74' },
		'2025-07-20': { time: '6:5', height: '1.89' },
		'2025-07-21': { time: '7:82', height: '1.88' },
		'2025-07-22': { time: '9:02', height: '1.72' },
		'2025-07-23': { time: '10:02', height: '1.49' },
		'2025-07-24': { time: '10:86', height: '1.27' },
		'2025-07-25': { time: '11:6', height: '1.09' },
		'2025-07-26': { time: '12:26', height: '0.99' },
		'2025-07-27': { time: '12:88', height: '0.97' },
		'2025-07-28': { time: '13:46', height: '1.04' },
		'2025-07-29': { time: '14:02', height: '1.17' },
		'2025-07-30': { time: '14:58', height: '1.36' },
		'2025-07-31': { time: '15:15', height: '1.58' },
		'2025-08-01': { time: '15:79', height: '1.83' },
		'2025-08-02': { time: '16:59', height: '2.07' },
		'2025-08-03': { time: '5:22', height: '2.39' },
		'2025-08-04': { time: '6:71', height: '2.49' },
		'2025-08-05': { time: '8:22', height: '2.37' },
		'2025-08-06': { time: '9:27', height: '2.1' },
		'2025-08-07': { time: '10:03', height: '1.78' },
		'2025-08-08': { time: '10:68', height: '1.44' },
		'2025-08-09': { time: '11:29', height: '1.14' },
		'2025-08-10': { time: '11:89', height: '0.91' },
		'2025-08-11': { time: '12:5', height: '0.76' },
		'2025-08-12': { time: '13:11', height: '0.72' },
		'2025-08-13': { time: '13:76', height: '0.79' },
		'2025-08-14': { time: '14:44', height: '0.98' },
		'2025-08-15': { time: '15:21', height: '1.25' },
		'2025-08-16': { time: '16:11', height: '1.57' },
		'2025-08-17': { time: '17:25', height: '1.86' },
		'2025-08-18': { time: '6:11', height: '2.16' },
		'2025-08-19': { time: '7:67', height: '2.17' },
		'2025-08-20': { time: '8:98', height: '1.95' },
		'2025-08-21': { time: '9:96', height: '1.65' },
		'2025-08-22': { time: '10:73', height: '1.36' },
		'2025-08-23': { time: '11:38', height: '1.15' },
		'2025-08-24': { time: '11:96', height: '1.03' },
		'2025-08-25': { time: '12:48', height: '0.99' },
		'2025-08-26': { time: '12:97', height: '1.04' },
		'2025-08-27': { time: '13:43', height: '1.15' },
		'2025-08-28': { time: '13:88', height: '1.31' },
		'2025-08-29': { time: '14:34', height: '1.52' },
		'2025-08-30': { time: '14:87', height: '1.76' },
		'2025-08-31': { time: '15:56', height: '2.03' },
		'2025-09-01': { time: '16:62', height: '2.28' },
		'2025-09-02': { time: '5:45', height: '2.55' },
		'2025-09-03': { time: '7:38', height: '2.49' },
		'2025-09-04': { time: '8:67', height: '2.17' },
		'2025-09-05': { time: '9:52', height: '1.77' },
		'2025-09-06': { time: '10:22', height: '1.36' },
		'2025-09-07': { time: '10:85', height: '1.01' },
		'2025-09-08': { time: '11:47', height: '0.74' },
		'2025-09-09': { time: '12:09', height: '0.59' },
		'2025-09-10': { time: '12:72', height: '0.57' },
		'2025-09-11': { time: '13:37', height: '0.68' },
		'2025-09-12': { time: '14:06', height: '0.92' },
		'2025-09-13': { time: '14:83', height: '1.26' },
		'2025-09-14': { time: '15:76', height: '1.64' },
		'2025-09-15': { time: '16:99', height: '1.97' },
		'2025-09-16': { time: '5:88', height: '2.3' },
		'2025-09-17': { time: '7:54', height: '2.27' },
		'2025-09-18': { time: '8:82', height: '2' },
		'2025-09-19': { time: '9:73', height: '1.68' },
		'2025-09-20': { time: '10:43', height: '1.41' },
		'2025-09-21': { time: '11:03', height: '1.21' },
		'2025-09-22': { time: '11:55', height: '1.11' },
		'2025-09-23': { time: '12:02', height: '1.09' },
		'2025-09-24': { time: '12:44', height: '1.13' },
		'2025-09-25': { time: '12:85', height: '1.22' },
		'2025-09-26': { time: '13:26', height: '1.36' },
		'2025-09-27': { time: '13:7', height: '1.53' },
		'2025-09-28': { time: '14:24', height: '1.74' },
		'2025-09-29': { time: '14:95', height: '1.99' },
		'2025-09-30': { time: '16:02', height: '2.24' },
		'2025-10-01': { time: '17:68', height: '2.34' },
		'2025-10-02': { time: '6:56', height: '2.42' },
		'2025-10-03': { time: '7:94', height: '2.12' },
		'2025-10-04': { time: '8:88', height: '1.72' },
		'2025-10-05': { time: '9:65', height: '1.31' },
		'2025-10-06': { time: '10:34', height: '0.95' },
		'2025-10-07': { time: '11:', height: '0.69' },
		'2025-10-08': { time: '11:66', height: '0.56' },
		'2025-10-09': { time: '12:32', height: '0.55' },
		'2025-10-10': { time: '13:01', height: '0.69' },
		'2025-10-11': { time: '13:75', height: '0.94' },
		'2025-10-12': { time: '14:57', height: '1.29' },
		'2025-10-13': { time: '15:56', height: '1.66' },
		'2025-10-14': { time: '16:84', height: '1.96' },
		'2025-10-15': { time: '5:63', height: '2.25' },
		'2025-10-16': { time: '7:17', height: '2.21' },
		'2025-10-17': { time: '8:38', height: '1.98' },
		'2025-10-18': { time: '9:28', height: '1.71' },
		'2025-10-19': { time: '9:99', height: '1.49' },
		'2025-10-20': { time: '10:58', height: '1.35' },
		'2025-10-21': { time: '11:09', height: '1.27' },
		'2025-10-22': { time: '11:55', height: '1.26' },
		'2025-10-23': { time: '11:96', height: '1.3' },
		'2025-10-24': { time: '12:37', height: '1.36' },
		'2025-10-25': { time: '12:8', height: '1.45' },
		'2025-10-26': { time: '13:29', height: '1.57' },
		'2025-10-27': { time: '13:89', height: '1.73' },
		'2025-10-28': { time: '14:67', height: '1.92' }
	};

	let valid_date = $derived.by(() => {
		let parsed_launch_date = Date.parse(launch_date);
		if (parsed_launch_date < parsed_min_date || parsed_launch_date > parsed_max_date) {
			return false;
		}
		return true;
	});

	let peak_time = $derived.by(() => {
		let time = tides[launch_date.valueOf()].time;
		let parts = time.split(':');
		let hours = parts[0];
		let mins = String(Math.round((parseInt(parts[1]) / 100) * 60));
		return hours.padStart(2, '0') + ':' + mins.padEnd(2, '0');
	});

	let peak_height = $derived(tides[launch_date.valueOf()].height);
</script>

<div class="m-auto h-full w-full max-w-lg p-4 text-left *:mx-auto">
	<div
		class="flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
	>
		<label for="date">Launch Date</label>
		<input
			type="date"
			bind:value={launch_date}
			min={min_date}
			max={max_date}
			id="date"
			class="w-fit"
		/>
	</div>

	{#if !valid_date}
		<div class="mt-8 text-lg">
			Sorry, I don't have any predictions for {launch_date}
		</div>
	{:else}
		<div class="mt-8 text-lg">
			My predictions for {launch_date}
		</div>

		<div
			class="mt-2 flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
		>
			<div>Peak Tide Time (UTC)</div>
			<div>{peak_time}</div>
		</div>
		<div
			class="mt-4 flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
		>
			<div>Peak Tide Height (m)</div>
			<div>{peak_height}</div>
		</div>
	{/if}
</div>
