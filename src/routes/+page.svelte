<script lang="ts">
	var today = new Date();
	var dd = String(today.getDate()).padStart(2, '0');
	var mm = String(today.getMonth() + 1).padStart(2, '0');
	var yyyy = today.getFullYear();

	let date = $state<string>(yyyy + '-' + mm + '-' + dd);

	let min_date = '2025-03-11';
	let max_date = '2025-10-28';

	let parsed_min_date = Date.parse(min_date);
	let parsed_max_date = Date.parse(max_date);

	// hard-coded data :D
	let tides: { [id: string]: { low_tide_time: string; low_tide_height: string; high_tide_height: string } } =
		{
			'2025-03-11': { low_tide_time: '9.8', low_tide_height: '1.5', high_tide_height: '4.7' },
			'2025-03-12': { low_tide_time: '10.52', low_tide_height: '1.2', high_tide_height: '4.9' },
			'2025-03-13': { low_tide_time: '11.11', low_tide_height: '1', high_tide_height: '5.1' },
			'2025-03-14': { low_tide_time: '11.62', low_tide_height: '1', high_tide_height: '5.1' },
			'2025-03-15': { low_tide_time: '12.08', low_tide_height: '1', high_tide_height: '5.1' },
			'2025-03-16': { low_tide_time: '12.49', low_tide_height: '1', high_tide_height: '5.1' },
			'2025-03-17': { low_tide_time: '12.89', low_tide_height: '1.2', high_tide_height: '5' },
			'2025-03-18': { low_tide_time: '13.3', low_tide_height: '1.3', high_tide_height: '4.9' },
			'2025-03-19': { low_tide_time: '13.75', low_tide_height: '1.4', high_tide_height: '4.8' },
			'2025-03-20': { low_tide_time: '14.28', low_tide_height: '1.6', high_tide_height: '4.6' },
			'2025-03-21': { low_tide_time: '14.96', low_tide_height: '1.9', high_tide_height: '4.4' },
			'2025-03-22': { low_tide_time: '15.93', low_tide_height: '2.1', high_tide_height: '4.2' },
			'2025-03-23': { low_tide_time: '17.4', low_tide_height: '2.3', high_tide_height: '4.1' },
			'2025-03-24': { low_tide_time: '6.4', low_tide_height: '2.1', high_tide_height: '4' },
			'2025-03-25': { low_tide_time: '7.86', low_tide_height: '1.9', high_tide_height: '4.3' },
			'2025-03-26': { low_tide_time: '8.88', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-03-27': { low_tide_time: '9.69', low_tide_height: '1.1', high_tide_height: '5.2' },
			'2025-03-28': { low_tide_time: '10.4', low_tide_height: '0.7', high_tide_height: '5.6' },
			'2025-03-29': { low_tide_time: '11.07', low_tide_height: '0.4', high_tide_height: '5.9' },
			'2025-03-30': { low_tide_time: '11.73', low_tide_height: '0.3', high_tide_height: '6' },
			'2025-03-31': { low_tide_time: '12.38', low_tide_height: '0.3', high_tide_height: '5.9' },
			'2025-04-01': { low_tide_time: '13.06', low_tide_height: '0.5', high_tide_height: '5.7' },
			'2025-04-02': { low_tide_time: '13.76', low_tide_height: '0.8', high_tide_height: '5.4' },
			'2025-04-03': { low_tide_time: '14.55', low_tide_height: '1.2', high_tide_height: '4.9' },
			'2025-04-04': { low_tide_time: '15.49', low_tide_height: '1.7', high_tide_height: '4.5' },
			'2025-04-05': { low_tide_time: '16.77', low_tide_height: '2.1', high_tide_height: '4.1' },
			'2025-04-06': { low_tide_time: '5.57', low_tide_height: '2', high_tide_height: '4.1' },
			'2025-04-07': { low_tide_time: '7.3', low_tide_height: '2', high_tide_height: '4.1' },
			'2025-04-08': { low_tide_time: '8.59', low_tide_height: '1.8', high_tide_height: '4.4' },
			'2025-04-09': { low_tide_time: '9.47', low_tide_height: '1.5', high_tide_height: '4.6' },
			'2025-04-10': { low_tide_time: '10.15', low_tide_height: '1.3', high_tide_height: '4.8' },
			'2025-04-11': { low_tide_time: '10.7', low_tide_height: '1.1', high_tide_height: '4.9' },
			'2025-04-12': { low_tide_time: '11.18', low_tide_height: '1.1', high_tide_height: '4.9' },
			'2025-04-13': { low_tide_time: '11.6', low_tide_height: '1.1', high_tide_height: '5' },
			'2025-04-14': { low_tide_time: '11.98', low_tide_height: '1.2', high_tide_height: '5' },
			'2025-04-15': { low_tide_time: '12.37', low_tide_height: '1.2', high_tide_height: '5' },
			'2025-04-16': { low_tide_time: '12.78', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-04-17': { low_tide_time: '13.26', low_tide_height: '1.4', high_tide_height: '4.9' },
			'2025-04-18': { low_tide_time: '13.83', low_tide_height: '1.5', high_tide_height: '4.7' },
			'2025-04-19': { low_tide_time: '14.56', low_tide_height: '1.7', high_tide_height: '4.5' },
			'2025-04-20': { low_tide_time: '15.56', low_tide_height: '1.9', high_tide_height: '4.3' },
			'2025-04-21': { low_tide_time: '16.93', low_tide_height: '2.1', high_tide_height: '4.2' },
			'2025-04-22': { low_tide_time: '5.86', low_tide_height: '2', high_tide_height: '4.1' },
			'2025-04-23': { low_tide_time: '7.24', low_tide_height: '1.8', high_tide_height: '4.4' },
			'2025-04-24': { low_tide_time: '8.31', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-04-25': { low_tide_time: '9.17', low_tide_height: '1.1', high_tide_height: '5.2' },
			'2025-04-26': { low_tide_time: '9.93', low_tide_height: '0.7', high_tide_height: '5.6' },
			'2025-04-27': { low_tide_time: '10.64', low_tide_height: '0.5', high_tide_height: '5.8' },
			'2025-04-28': { low_tide_time: '11.34', low_tide_height: '0.4', high_tide_height: '5.9' },
			'2025-04-29': { low_tide_time: '12.03', low_tide_height: '0.4', high_tide_height: '5.8' },
			'2025-04-30': { low_tide_time: '12.74', low_tide_height: '0.6', high_tide_height: '5.6' },
			'2025-05-01': { low_tide_time: '13.48', low_tide_height: '0.9', high_tide_height: '5.3' },
			'2025-05-02': { low_tide_time: '14.3', low_tide_height: '1.2', high_tide_height: '4.9' },
			'2025-05-03': { low_tide_time: '15.25', low_tide_height: '1.6', high_tide_height: '4.6' },
			'2025-05-04': { low_tide_time: '16.44', low_tide_height: '2', high_tide_height: '4.3' },
			'2025-05-05': { low_tide_time: '5.11', low_tide_height: '1.9', high_tide_height: '4.1' },
			'2025-05-06': { low_tide_time: '6.74', low_tide_height: '2', high_tide_height: '4.1' },
			'2025-05-07': { low_tide_time: '7.98', low_tide_height: '1.8', high_tide_height: '4.2' },
			'2025-05-08': { low_tide_time: '8.9', low_tide_height: '1.6', high_tide_height: '4.4' },
			'2025-05-09': { low_tide_time: '9.61', low_tide_height: '1.5', high_tide_height: '4.5' },
			'2025-05-10': { low_tide_time: '10.19', low_tide_height: '1.4', high_tide_height: '4.7' },
			'2025-05-11': { low_tide_time: '10.68', low_tide_height: '1.3', high_tide_height: '4.7' },
			'2025-05-12': { low_tide_time: '11.12', low_tide_height: '1.3', high_tide_height: '4.8' },
			'2025-05-13': { low_tide_time: '11.54', low_tide_height: '1.3', high_tide_height: '4.9' },
			'2025-05-14': { low_tide_time: '11.97', low_tide_height: '1.3', high_tide_height: '4.9' },
			'2025-05-15': { low_tide_time: '12.45', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-05-16': { low_tide_time: '12.99', low_tide_height: '1.4', high_tide_height: '4.9' },
			'2025-05-17': { low_tide_time: '13.63', low_tide_height: '1.4', high_tide_height: '4.8' },
			'2025-05-18': { low_tide_time: '14.41', low_tide_height: '1.6', high_tide_height: '4.7' },
			'2025-05-19': { low_tide_time: '15.36', low_tide_height: '1.7', high_tide_height: '4.6' },
			'2025-05-20': { low_tide_time: '16.53', low_tide_height: '1.8', high_tide_height: '4.5' },
			'2025-05-21': { low_tide_time: '5.3', low_tide_height: '1.8', high_tide_height: '4.4' },
			'2025-05-22': { low_tide_time: '6.56', low_tide_height: '1.7', high_tide_height: '4.5' },
			'2025-05-23': { low_tide_time: '7.67', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-05-24': { low_tide_time: '8.63', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-05-25': { low_tide_time: '9.49', low_tide_height: '0.9', high_tide_height: '5.3' },
			'2025-05-26': { low_tide_time: '10.27', low_tide_height: '0.7', high_tide_height: '5.5' },
			'2025-05-27': { low_tide_time: '11.03', low_tide_height: '0.6', high_tide_height: '5.6' },
			'2025-05-28': { low_tide_time: '11.78', low_tide_height: '0.6', high_tide_height: '5.6' },
			'2025-05-29': { low_tide_time: '12.52', low_tide_height: '0.8', high_tide_height: '5.4' },
			'2025-05-30': { low_tide_time: '13.29', low_tide_height: '1', high_tide_height: '5.2' },
			'2025-05-31': { low_tide_time: '14.09', low_tide_height: '1.2', high_tide_height: '5' },
			'2025-06-01': { low_tide_time: '14.96', low_tide_height: '1.5', high_tide_height: '4.7' },
			'2025-06-02': { low_tide_time: '15.94', low_tide_height: '1.8', high_tide_height: '4.5' },
			'2025-06-03': { low_tide_time: '17.05', low_tide_height: '2', high_tide_height: '4.3' },
			'2025-06-04': { low_tide_time: '5.85', low_tide_height: '1.9', high_tide_height: '4.1' },
			'2025-06-05': { low_tide_time: '7.06', low_tide_height: '2', high_tide_height: '4.1' },
			'2025-06-06': { low_tide_time: '8.1', low_tide_height: '1.9', high_tide_height: '4.1' },
			'2025-06-07': { low_tide_time: '8.93', low_tide_height: '1.8', high_tide_height: '4.3' },
			'2025-06-08': { low_tide_time: '9.6', low_tide_height: '1.7', high_tide_height: '4.4' },
			'2025-06-09': { low_tide_time: '10.18', low_tide_height: '1.7', high_tide_height: '4.5' },
			'2025-06-10': { low_tide_time: '10.69', low_tide_height: '1.6', high_tide_height: '4.7' },
			'2025-06-11': { low_tide_time: '11.2', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-06-12': { low_tide_time: '11.72', low_tide_height: '1.4', high_tide_height: '5' },
			'2025-06-13': { low_tide_time: '12.27', low_tide_height: '1.3', high_tide_height: '5.1' },
			'2025-06-14': { low_tide_time: '12.88', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-06-15': { low_tide_time: '13.55', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-06-16': { low_tide_time: '14.29', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-06-17': { low_tide_time: '15.13', low_tide_height: '1.4', high_tide_height: '4.9' },
			'2025-06-18': { low_tide_time: '16.09', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-06-19': { low_tide_time: '17.18', low_tide_height: '1.6', high_tide_height: '4.7' },
			'2025-06-20': { low_tide_time: '5.86', low_tide_height: '1.7', high_tide_height: '4.6' },
			'2025-06-21': { low_tide_time: '7.04', low_tide_height: '1.6', high_tide_height: '4.6' },
			'2025-06-22': { low_tide_time: '8.15', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-06-23': { low_tide_time: '9.15', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-06-24': { low_tide_time: '10.04', low_tide_height: '1.1', high_tide_height: '5.2' },
			'2025-06-25': { low_tide_time: '10.87', low_tide_height: '1', high_tide_height: '5.3' },
			'2025-06-26': { low_tide_time: '11.64', low_tide_height: '0.9', high_tide_height: '5.4' },
			'2025-06-27': { low_tide_time: '12.38', low_tide_height: '0.9', high_tide_height: '5.4' },
			'2025-06-28': { low_tide_time: '13.1', low_tide_height: '1', high_tide_height: '5.3' },
			'2025-06-29': { low_tide_time: '13.81', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-06-30': { low_tide_time: '14.53', low_tide_height: '1.4', high_tide_height: '5' },
			'2025-07-01': { low_tide_time: '15.29', low_tide_height: '1.6', high_tide_height: '4.7' },
			'2025-07-02': { low_tide_time: '16.11', low_tide_height: '1.8', high_tide_height: '4.5' },
			'2025-07-03': { low_tide_time: '17.04', low_tide_height: '2', high_tide_height: '4.3' },
			'2025-07-04': { low_tide_time: '5.83', low_tide_height: '2.1', high_tide_height: '4' },
			'2025-07-05': { low_tide_time: '6.97', low_tide_height: '2.2', high_tide_height: '3.9' },
			'2025-07-06': { low_tide_time: '8.06', low_tide_height: '2.2', high_tide_height: '4' },
			'2025-07-07': { low_tide_time: '8.95', low_tide_height: '2.1', high_tide_height: '4.2' },
			'2025-07-08': { low_tide_time: '9.69', low_tide_height: '1.9', high_tide_height: '4.4' },
			'2025-07-09': { low_tide_time: '10.34', low_tide_height: '1.7', high_tide_height: '4.7' },
			'2025-07-10': { low_tide_time: '10.93', low_tide_height: '1.5', high_tide_height: '4.9' },
			'2025-07-11': { low_tide_time: '11.52', low_tide_height: '1.3', high_tide_height: '5.1' },
			'2025-07-12': { low_tide_time: '12.12', low_tide_height: '1.1', high_tide_height: '5.3' },
			'2025-07-13': { low_tide_time: '12.74', low_tide_height: '1', high_tide_height: '5.4' },
			'2025-07-14': { low_tide_time: '13.38', low_tide_height: '0.9', high_tide_height: '5.4' },
			'2025-07-15': { low_tide_time: '14.06', low_tide_height: '1', high_tide_height: '5.3' },
			'2025-07-16': { low_tide_time: '14.8', low_tide_height: '1.1', high_tide_height: '5.2' },
			'2025-07-17': { low_tide_time: '15.63', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-07-18': { low_tide_time: '16.59', low_tide_height: '1.5', high_tide_height: '4.8' },
			'2025-07-19': { low_tide_time: '5.22', low_tide_height: '1.7', high_tide_height: '4.6' },
			'2025-07-20': { low_tide_time: '6.48', low_tide_height: '1.9', high_tide_height: '4.4' },
			'2025-07-21': { low_tide_time: '7.81', low_tide_height: '1.8', high_tide_height: '4.5' },
			'2025-07-22': { low_tide_time: '8.99', low_tide_height: '1.7', high_tide_height: '4.7' },
			'2025-07-23': { low_tide_time: '9.98', low_tide_height: '1.4', high_tide_height: '4.9' },
			'2025-07-24': { low_tide_time: '10.81', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-07-25': { low_tide_time: '11.54', low_tide_height: '1.1', high_tide_height: '5.3' },
			'2025-07-26': { low_tide_time: '12.21', low_tide_height: '1', high_tide_height: '5.4' },
			'2025-07-27': { low_tide_time: '12.83', low_tide_height: '1', high_tide_height: '5.4' },
			'2025-07-28': { low_tide_time: '13.42', low_tide_height: '1.1', high_tide_height: '5.3' },
			'2025-07-29': { low_tide_time: '14', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-07-30': { low_tide_time: '14.59', low_tide_height: '1.4', high_tide_height: '4.9' },
			'2025-07-31': { low_tide_time: '15.21', low_tide_height: '1.6', high_tide_height: '4.6' },
			'2025-08-01': { low_tide_time: '15.92', low_tide_height: '1.8', high_tide_height: '4.4' },
			'2025-08-02': { low_tide_time: '16.82', low_tide_height: '2.1', high_tide_height: '4.1' },
			'2025-08-03': { low_tide_time: '5.55', low_tide_height: '2.4', high_tide_height: '3.9' },
			'2025-08-04': { low_tide_time: '6.92', low_tide_height: '2.5', high_tide_height: '3.9' },
			'2025-08-05': { low_tide_time: '8.23', low_tide_height: '2.4', high_tide_height: '4.1' },
			'2025-08-06': { low_tide_time: '9.21', low_tide_height: '2.1', high_tide_height: '4.4' },
			'2025-08-07': { low_tide_time: '9.97', low_tide_height: '1.8', high_tide_height: '4.7' },
			'2025-08-08': { low_tide_time: '10.63', low_tide_height: '1.4', high_tide_height: '5.1' },
			'2025-08-09': { low_tide_time: '11.25', low_tide_height: '1.1', high_tide_height: '5.4' },
			'2025-08-10': { low_tide_time: '11.85', low_tide_height: '0.8', high_tide_height: '5.6' },
			'2025-08-11': { low_tide_time: '12.46', low_tide_height: '0.7', high_tide_height: '5.7' },
			'2025-08-12': { low_tide_time: '13.09', low_tide_height: '0.6', high_tide_height: '5.7' },
			'2025-08-13': { low_tide_time: '13.73', low_tide_height: '0.7', high_tide_height: '5.6' },
			'2025-08-14': { low_tide_time: '14.42', low_tide_height: '0.9', high_tide_height: '5.4' },
			'2025-08-15': { low_tide_time: '15.18', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-08-16': { low_tide_time: '16.09', low_tide_height: '1.6', high_tide_height: '4.7' },
			'2025-08-17': { low_tide_time: '17.25', low_tide_height: '1.9', high_tide_height: '4.5' },
			'2025-08-18': { low_tide_time: '6.08', low_tide_height: '2.1', high_tide_height: '4.3' },
			'2025-08-19': { low_tide_time: '7.69', low_tide_height: '2.1', high_tide_height: '4.3' },
			'2025-08-20': { low_tide_time: '9.01', low_tide_height: '1.9', high_tide_height: '4.5' },
			'2025-08-21': { low_tide_time: '9.97', low_tide_height: '1.6', high_tide_height: '4.8' },
			'2025-08-22': { low_tide_time: '10.72', low_tide_height: '1.4', high_tide_height: '5.1' },
			'2025-08-23': { low_tide_time: '11.36', low_tide_height: '1.2', high_tide_height: '5.3' },
			'2025-08-24': { low_tide_time: '11.93', low_tide_height: '1', high_tide_height: '5.4' },
			'2025-08-25': { low_tide_time: '12.45', low_tide_height: '1', high_tide_height: '5.4' },
			'2025-08-26': { low_tide_time: '12.95', low_tide_height: '1', high_tide_height: '5.4' },
			'2025-08-27': { low_tide_time: '13.43', low_tide_height: '1.1', high_tide_height: '5.2' },
			'2025-08-28': { low_tide_time: '13.91', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-08-29': { low_tide_time: '14.43', low_tide_height: '1.5', high_tide_height: '4.7' },
			'2025-08-30': { low_tide_time: '15.04', low_tide_height: '1.7', high_tide_height: '4.4' },
			'2025-08-31': { low_tide_time: '15.82', low_tide_height: '2', high_tide_height: '4.1' },
			'2025-09-01': { low_tide_time: '16.98', low_tide_height: '2.3', high_tide_height: '3.9' },
			'2025-09-02': { low_tide_time: '5.7', low_tide_height: '2.6', high_tide_height: '3.9' },
			'2025-09-03': { low_tide_time: '7.41', low_tide_height: '2.5', high_tide_height: '4.1' },
			'2025-09-04': { low_tide_time: '8.64', low_tide_height: '2.2', high_tide_height: '4.4' },
			'2025-09-05': { low_tide_time: '9.5', low_tide_height: '1.7', high_tide_height: '4.9' },
			'2025-09-06': { low_tide_time: '10.2', low_tide_height: '1.3', high_tide_height: '5.3' },
			'2025-09-07': { low_tide_time: '10.85', low_tide_height: '0.9', high_tide_height: '5.6' },
			'2025-09-08': { low_tide_time: '11.47', low_tide_height: '0.6', high_tide_height: '5.9' },
			'2025-09-09': { low_tide_time: '12.09', low_tide_height: '0.5', high_tide_height: '6' },
			'2025-09-10': { low_tide_time: '12.71', low_tide_height: '0.4', high_tide_height: '6' },
			'2025-09-11': { low_tide_time: '13.36', low_tide_height: '0.6', high_tide_height: '5.8' },
			'2025-09-12': { low_tide_time: '14.04', low_tide_height: '0.8', high_tide_height: '5.5' },
			'2025-09-13': { low_tide_time: '14.81', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-09-14': { low_tide_time: '15.73', low_tide_height: '1.6', high_tide_height: '4.7' },
			'2025-09-15': { low_tide_time: '16.99', low_tide_height: '2', high_tide_height: '4.3' },
			'2025-09-16': { low_tide_time: '5.87', low_tide_height: '2.3', high_tide_height: '4.2' },
			'2025-09-17': { low_tide_time: '7.64', low_tide_height: '2.3', high_tide_height: '4.2' },
			'2025-09-18': { low_tide_time: '8.91', low_tide_height: '2', high_tide_height: '4.5' },
			'2025-09-19': { low_tide_time: '9.78', low_tide_height: '1.7', high_tide_height: '4.9' },
			'2025-09-20': { low_tide_time: '10.46', low_tide_height: '1.4', high_tide_height: '5.1' },
			'2025-09-21': { low_tide_time: '11.03', low_tide_height: '1.2', high_tide_height: '5.3' },
			'2025-09-22': { low_tide_time: '11.54', low_tide_height: '1.1', high_tide_height: '5.4' },
			'2025-09-23': { low_tide_time: '12', low_tide_height: '1.1', high_tide_height: '5.4' },
			'2025-09-24': { low_tide_time: '12.44', low_tide_height: '1.1', high_tide_height: '5.3' },
			'2025-09-25': { low_tide_time: '12.87', low_tide_height: '1.2', high_tide_height: '5.2' },
			'2025-09-26': { low_tide_time: '13.32', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-09-27': { low_tide_time: '13.82', low_tide_height: '1.4', high_tide_height: '4.8' },
			'2025-09-28': { low_tide_time: '14.41', low_tide_height: '1.7', high_tide_height: '4.5' },
			'2025-09-29': { low_tide_time: '15.18', low_tide_height: '1.9', high_tide_height: '4.2' },
			'2025-09-30': { low_tide_time: '16.3', low_tide_height: '2.2', high_tide_height: '4' },
			'2025-10-01': { low_tide_time: '17.92', low_tide_height: '2.3', high_tide_height: '4' },
			'2025-10-02': { low_tide_time: '6.59', low_tide_height: '2.4', high_tide_height: '4.2' },
			'2025-10-03': { low_tide_time: '7.95', low_tide_height: '2.1', high_tide_height: '4.6' },
			'2025-10-04': { low_tide_time: '8.9', low_tide_height: '1.6', high_tide_height: '5' },
			'2025-10-05': { low_tide_time: '9.67', low_tide_height: '1.2', high_tide_height: '5.4' },
			'2025-10-06': { low_tide_time: '10.36', low_tide_height: '0.8', high_tide_height: '5.7' },
			'2025-10-07': { low_tide_time: '11.02', low_tide_height: '0.6', high_tide_height: '6' },
			'2025-10-08': { low_tide_time: '11.67', low_tide_height: '0.4', high_tide_height: '6.1' },
			'2025-10-09': { low_tide_time: '12.33', low_tide_height: '0.4', high_tide_height: '6' },
			'2025-10-10': { low_tide_time: '13.01', low_tide_height: '0.6', high_tide_height: '5.8' },
			'2025-10-11': { low_tide_time: '13.73', low_tide_height: '0.9', high_tide_height: '5.5' },
			'2025-10-12': { low_tide_time: '14.54', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-10-13': { low_tide_time: '15.52', low_tide_height: '1.7', high_tide_height: '4.6' },
			'2025-10-14': { low_tide_time: '16.85', low_tide_height: '2', high_tide_height: '4.3' },
			'2025-10-15': { low_tide_time: '5.66', low_tide_height: '2.3', high_tide_height: '4.2' },
			'2025-10-16': { low_tide_time: '7.3', low_tide_height: '2.2', high_tide_height: '4.3' },
			'2025-10-17': { low_tide_time: '8.51', low_tide_height: '2', high_tide_height: '4.6' },
			'2025-10-18': { low_tide_time: '9.36', low_tide_height: '1.7', high_tide_height: '4.9' },
			'2025-10-19': { low_tide_time: '10.03', low_tide_height: '1.5', high_tide_height: '5.1' },
			'2025-10-20': { low_tide_time: '10.59', low_tide_height: '1.4', high_tide_height: '5.2' },
			'2025-10-21': { low_tide_time: '11.08', low_tide_height: '1.3', high_tide_height: '5.2' },
			'2025-10-22': { low_tide_time: '11.54', low_tide_height: '1.2', high_tide_height: '5.2' },
			'2025-10-23': { low_tide_time: '11.97', low_tide_height: '1.2', high_tide_height: '5.1' },
			'2025-10-24': { low_tide_time: '12.4', low_tide_height: '1.3', high_tide_height: '5' },
			'2025-10-25': { low_tide_time: '12.87', low_tide_height: '1.4', high_tide_height: '4.9' },
			'2025-10-26': { low_tide_time: '13.4', low_tide_height: '1.5', high_tide_height: '4.7' },
			'2025-10-27': { low_tide_time: '14.03', low_tide_height: '1.7', high_tide_height: '4.5' },
			'2025-10-28': { low_tide_time: '14.83', low_tide_height: '1.9', high_tide_height: '4.3' }
		};

	let valid_date = $derived.by(() => {
		let parsed_launch_date = Date.parse(date);
		if (parsed_launch_date < parsed_min_date || parsed_launch_date > parsed_max_date) {
			return false;
		}
		return true;
	});

	// time is stored as a float in hours, this does the conversion
	function convert_hours_to_time(hours: number) {
		let whole_hours = Math.trunc(hours)
		let mins = Math.round((whole_hours-whole_hours)*60)
		return whole_hours.toString() + ':' + mins.toString().padStart(2, '0');
	}

	let low_time = $derived.by(() => {
		let hours = parseFloat(tides[date.valueOf()].low_tide_time);
		return convert_hours_to_time(hours);
	});

	let high_time = $derived.by(() => {
		let hours = parseFloat(tides[date.valueOf()].low_tide_time) + 6.2; // hacky fix, adds 6hrs and 12 mins to the low tide time
		return convert_hours_to_time(hours);
	});

	let low_tide_height = $derived(tides[date.valueOf()].low_tide_height);
	let high_tide_height = $derived(tides[date.valueOf()].high_tide_height);
</script>

<svelte:head>
	<title>Newlyn Tides</title>
</svelte:head>

<div class="m-auto h-full w-full max-w-lg p-4 text-left *:mx-auto">
	<div
		class="flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
	>
		<label for="date">Date</label>
		<input type="date" bind:value={date} min={min_date} max={max_date} id="date" class="w-fit" />
	</div>

	{#if !valid_date}
		<div class="mt-8 text-lg">
			Sorry, I don't have any predictions for {date}
		</div>
	{:else}
		<div class="mt-8 text-lg">
			My predictions for {date}
		</div>

		<div
			class="mt-2 flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
		>
			<div>Time of low tide (UTC)</div>
			<div>{low_time}</div>
		</div>
		<div
			class="mt-4 flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
		>
			<div>Height of low tide (m)</div>
			<div>{low_tide_height}</div>
		</div>

		<div
			class="mt-4 flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
		>
			<div>Time of high tide (UTC)</div>
			<div>{high_time}</div>
		</div>
		<div
			class="mt-4 flex w-full flex-row items-center justify-between gap-2 rounded-lg border border-gray-400 p-2"
		>
			<div>Height of high tide (m)</div>
			<div>{high_tide_height}</div>
		</div>
	{/if}
</div>
