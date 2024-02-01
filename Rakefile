task :update_itinerary do
  require 'google/apis/sheets_v4'
  require 'googleauth'

  # Load credentials  
  credentials = Google::Auth::ServiceAccountCredentials.make_creds(
    json_key_io: File.open('./sheets-api-key.json'),
    scope: Google::Apis::SheetsV4::AUTH_SPREADSHEETS_READONLY
  )

  # Authorize the client
  service = Google::Apis::SheetsV4::SheetsService.new
  service.authorization = credentials


  spreadsheet_id = '14q0flcNjGJRw7706Y-3hu571JBuPWIU4JsjUb488YZc'
  range = 'EVERYDAY!A1:B400'

  response = service.get_spreadsheet_values(spreadsheet_id, range)
  data = response.values

  markdown_table = '| ' + data[0].join(' | ') + " |\n" +
                 '| ' + ('---' * data[0].length) + " |\n" +
                 data[1..].map { |row| '| ' + row.join(' | ') + ' |' }.join("\n")
  
  File.write('_includes/itinerary_sheet.md', markdown_table)
end