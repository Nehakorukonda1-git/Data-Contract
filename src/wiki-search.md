```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LifeChurch Data Contract Wiki</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 40px 20px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-size: 3em;
            margin-bottom: 10px;
        }

        .header h1 {
            font-size: 2.5em;
            color: #667eea;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .header .subtitle {
            font-size: 1.2em;
            color: #666;
            margin-bottom: 30px;
        }

        .search-container {
            max-width: 800px;
            margin: 0 auto;
            position: relative;
        }

        #searchInput {
            width: 100%;
            padding: 20px 60px 20px 25px;
            font-size: 20px;
            border: 3px solid #667eea;
            border-radius: 50px;
            outline: none;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.2);
        }

        #searchInput:focus {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
            border-color: #764ba2;
        }

        .search-icon {
            position: absolute;
            right: 25px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 24px;
            color: #667eea;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        .stats-bar {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .stat-card {
            background: rgba(255, 255, 255, 0.95);
            padding: 20px 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        .stat-number {
            font-size: 2em;
            font-weight: 700;
            color: #667eea;
        }

        .stat-label {
            font-size: 0.9em;
            color: #666;
            margin-top: 5px;
        }

        #results {
            margin-top: 30px;
        }

        .contract-card {
            background: rgba(255, 255, 255, 0.98);
            padding: 30px;
            margin-bottom: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            border-left: 6px solid #667eea;
            transition: all 0.3s ease;
            cursor: pointer;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .contract-card:hover {
            transform: translateX(5px);
            box-shadow: 0 6px 30px rgba(0, 0, 0, 0.15);
            border-left-color: #764ba2;
        }

        .contract-card.expanded {
            border-left-color: #764ba2;
            background: linear-gradient(135deg, rgba(255,255,255,0.98) 0%, rgba(240,242,255,0.98) 100%);
        }

        .contract-card.view-card {
            border-left-color: #ff6b6b;
        }

        .contract-card.view-card:hover {
            border-left-color: #ee5a5a;
        }

        .contract-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .contract-name {
            font-size: 1.8em;
            font-weight: 700;
            color: #667eea;
            font-family: 'Courier New', monospace;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .view-card .contract-name {
            color: #ff6b6b;
        }

        .contract-badge {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 6px 15px;
            border-radius: 20px;
            font-size: 0.5em;
            font-weight: 600;
            letter-spacing: 0.5px;
        }

        .view-card .contract-badge {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a5a 100%);
        }

        .contract-description {
            font-size: 1.15em;
            color: #555;
            line-height: 1.8;
            margin-bottom: 20px;
        }

        .contract-meta {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 2px solid #f0f0f0;
        }

        .meta-item {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .meta-label {
            font-size: 0.85em;
            color: #999;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
        }

        .meta-value {
            font-size: 1.1em;
            color: #333;
            font-weight: 600;
        }

        .contract-details {
            display: none;
            margin-top: 25px;
            padding-top: 25px;
            border-top: 2px solid #e8e8ff;
        }

        .contract-details.visible {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .detail-section {
            margin-bottom: 25px;
            background: rgba(255, 255, 255, 0.6);
            padding: 20px;
            border-radius: 10px;
        }

        .detail-title {
            font-size: 1.2em;
            font-weight: 700;
            color: #667eea;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .detail-content {
            font-size: 1.05em;
            color: #555;
            line-height: 1.8;
        }

        .examples-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }

        .example-item {
            background: #f8f9ff;
            padding: 12px 18px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            border-left: 3px solid #667eea;
            font-weight: 600;
        }

        .rules-list {
            list-style: none;
            padding: 0;
        }

        .rules-list li {
            padding: 10px 15px;
            margin-bottom: 8px;
            background: #f8f9ff;
            border-left: 3px solid #764ba2;
            border-radius: 5px;
        }

        .rules-list li:before {
            content: "✓ ";
            color: #667eea;
            font-weight: bold;
            margin-right: 8px;
        }

        .columns-table {
            width: 100%;
            background: white;
            border-radius: 8px;
            overflow: hidden;
        }

        .columns-table th,
        .columns-table td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #f0f0f0;
        }

        .columns-table th {
            background: #f8f9ff;
            font-weight: 700;
            color: #667eea;
        }

        .columns-table td {
            color: #555;
        }

        .no-results {
            text-align: center;
            padding: 80px 20px;
            color: white;
        }

        .no-results-icon {
            font-size: 5em;
            margin-bottom: 20px;
            opacity: 0.8;
        }

        .no-results h3 {
            font-size: 1.8em;
            margin-bottom: 15px;
        }

        .no-results p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .toggle-icon {
            font-size: 1.2em;
            transition: transform 0.3s ease;
        }

        .contract-card.expanded .toggle-icon {
            transform: rotate(180deg);
        }

        .quick-search-tips {
            text-align: center;
            color: white;
            margin-top: 20px;
            font-size: 0.9em;
            opacity: 0.9;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.8em;
            }
            
            .contract-name {
                font-size: 1.3em;
            }
            
            .stats-bar {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <div class="logo">🔍</div>
        <h1>LifeChurch Data Contract Wiki</h1>
        <p class="subtitle">Instant search for views and columns</p>
        
        <div class="search-container">
            <input 
                type="text" 
                id="searchInput" 
                placeholder="Type: known_step_view, campus, rms_person_id..."
                autocomplete="off"
                autofocus
            />
            <span class="search-icon">🔍</span>
        </div>
    </div>

    <div class="container">
        <div class="stats-bar">
            <div class="stat-card">
                <div class="stat-number">1</div>
                <div class="stat-label">Views</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">14</div>
                <div class="stat-label">Columns</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="resultsCount">15</div>
                <div class="stat-label">Total Contracts</div>
            </div>
        </div>

        <div id="results"></div>

        <div class="quick-search-tips">
            💡 Tip: Search is exact-match focused. Try "campus", "known_step_view", or "rms_person_id"
        </div>
    </div>

    <script>
        const dataContracts = [
            {
                type: "view",
                name: "known_step_view",
                database: "analytics",
                schema: "analytics",
                description: "This view tracks individuals who are new to LifeChurch and have attended a Known event, capturing their engagement journey including which campus they attended, their full name and RMS ID, the step type they took after the event (such as Chose Next Step or Indicated Interest), and whether that step has been completed or started. This model helps pastors track and follow up with new attendees, monitor their progress through next steps, and measure the overall success and effectiveness of Known events across campuses.",
                owner: "Data Insights Team",
                tags: ["analytics"],
                uniqueKey: ["known_step_guid"],
                nonNull: ["rms_person_id"],
                columns: [
                    "known_step_guid", "known_step_id", "rms_person_id", "primary_person_alias",
                    "name", "known_step_type_name", "known_step_status", "campus",
                    "start_date_time", "known_class_date", "known_class_size", "known_category",
                    "known_next_step", "known_step_note"
                ]
            },
            {
                type: "column",
                name: "known_step_guid",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.guid",
                description: "Unique identifier (GUID) for each step record in the Known event tracking system",
                owner: "Data Insights Team",
                examples: ["a1b2c3d4-e5f6-7890-abcd-ef1234567890", "f9e8d7c6-b5a4-3210-9876-543210fedcba"],
                usage: "Primary key for uniquely identifying each Known event step record. Used for joining with other tables and ensuring data integrity.",
                businessRules: [
                    "Must be unique across all records",
                    "Cannot be null (Primary Key)",
                    "Automatically generated on record creation",
                    "UUID format (universally unique identifier)"
                ],
                assertions: "Unique Key"
            },
            {
                type: "column",
                name: "known_step_id",
                viewName: "known_step_view",
                dataType: "INTEGER",
                source: "docs.columns.step_id",
                description: "Numeric identifier for the step taken by an attendee after a Known event",
                owner: "Data Insights Team",
                examples: ["1", "2", "3", "45", "67"],
                usage: "Secondary identifier for step records. Can be used for sorting and numeric operations.",
                businessRules: [
                    "Numeric identifier",
                    "May not be unique (multiple records can share same step_id)",
                    "Used in conjunction with GUID for complete identification"
                ]
            },
            {
                type: "column",
                name: "rms_person_id",
                viewName: "known_step_view",
                dataType: "INTEGER",
                source: "docs.columns.rms_person_id",
                description: "Person's unique identifier in the Rock Management System (RMS), linking Known event data to individual person records",
                owner: "Data Insights Team",
                examples: ["12345", "67890", "11223", "98765"],
                usage: "Critical foreign key for joining with person-related tables. Links Known event engagement to individual attendee profiles.",
                businessRules: [
                    "Cannot be null (required field)",
                    "Must exist in RMS person table",
                    "Used as foreign key in multiple joins",
                    "Links to master person record"
                ],
                assertions: "Non-Null"
            },
            {
                type: "column",
                name: "primary_person_alias",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.primary_person_alias",
                description: "Primary alias or alternative identifier for a person in the system, often used for system-level identification",
                owner: "Data Insights Team",
                examples: ["john.doe", "jane.smith", "pastor.mike", "volunteer123"],
                usage: "Alternative identifier for person records. Useful when email or username is the primary lookup method.",
                businessRules: [
                    "May be used as alternative login identifier",
                    "Should be unique per person",
                    "Often corresponds to email prefix or username"
                ]
            },
            {
                type: "column",
                name: "name",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.full_name",
                description: "Full name of the person who attended the Known event, combining first and last name",
                owner: "Data Insights Team",
                examples: ["John Doe", "Jane Smith", "Michael Johnson", "Sarah Williams"],
                usage: "Display name for reports, dashboards, and pastor follow-up lists. Human-readable identifier.",
                businessRules: [
                    "Contains first and last name",
                    "Used in pastor communication and follow-up",
                    "May include middle name or initial",
                    "Should match legal name when possible"
                ]
            },
            {
                type: "column",
                name: "known_step_type_name",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.known_step_type",
                description: "Type or category of the next step taken by the attendee after the Known event (e.g., Chose Next Step, Indicated Interest)",
                owner: "Data Insights Team",
                examples: ["Chose Next Step", "Indicated Interest", "Requested Follow-Up", "Joined Small Group"],
                usage: "Categorizes the type of engagement action. Critical for understanding attendee intent and routing follow-ups.",
                businessRules: [
                    "Limited to predefined step types",
                    "Used for filtering and categorization",
                    "Determines follow-up workflow",
                    "Impacts next step assignment logic"
                ]
            },
            {
                type: "column",
                name: "known_step_status",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.known_step_status",
                description: "Current status of the step (e.g., Completed, Started, Pending), tracking progress through the Known event follow-up process",
                owner: "Data Insights Team",
                examples: ["Completed", "Started", "Pending", "In Progress", "Not Started"],
                usage: "Tracks completion progress. Essential for pastor dashboards showing who needs follow-up versus who has completed their next steps.",
                businessRules: [
                    "Must be one of predefined status values",
                    "Updated as attendee progresses",
                    "Used in completion metrics",
                    "Triggers automated follow-up workflows"
                ]
            },
            {
                type: "column",
                name: "campus",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.campus",
                description: "LifeChurch campus location where the Known event was attended, identifying the specific church site",
                owner: "Data Insights Team",
                examples: ["Oklahoma City", "Edmond", "Stillwater", "Tulsa", "Norman", "Broken Arrow", "Midwest City", "Moore", "Yukon"],
                usage: "Critical for campus-level reporting, pastor follow-up routing by location, and geographic engagement analysis.",
                businessRules: [
                    "Must be valid LifeChurch campus name",
                    "Used for routing follow-ups to campus pastors",
                    "Essential for campus-specific dashboards",
                    "Links to campus master data"
                ]
            },
            {
                type: "column",
                name: "start_date_time",
                viewName: "known_step_view",
                dataType: "TIMESTAMP",
                source: "docs.columns.start_timestamp",
                description: "Date and time when the Known event step was initiated or started by the attendee",
                owner: "Data Insights Team",
                examples: ["2024-11-01 14:30:00", "2024-10-15 09:15:00", "2024-11-20 18:45:00"],
                usage: "Tracks when engagement began. Used for time-based analysis, follow-up timing, and measuring time-to-completion.",
                businessRules: [
                    "Timestamp format with date and time",
                    "Used for chronological sorting",
                    "Determines follow-up timing windows",
                    "Critical for time-based metrics"
                ]
            },
            {
                type: "column",
                name: "known_class_date",
                viewName: "known_step_view",
                dataType: "DATE",
                source: "docs.columns.known_class_date",
                description: "The specific date when the Known class or event was held at the campus",
                owner: "Data Insights Team",
                examples: ["2024-11-01", "2024-10-15", "2024-11-20"],
                usage: "Identifies which Known class session the attendee participated in. Used for class-level attendance tracking.",
                businessRules: [
                    "Date format (no time component)",
                    "Links multiple attendees to same class session",
                    "Used for class attendance reports",
                    "Groups attendees by class cohort"
                ]
            },
            {
                type: "column",
                name: "known_class_size",
                viewName: "known_step_view",
                dataType: "INTEGER",
                source: "docs.columns.known_class_size",
                description: "Total number of attendees who participated in the Known class session",
                owner: "Data Insights Team",
                examples: ["15", "20", "30", "45", "8"],
                usage: "Tracks class capacity and attendance levels. Used for capacity planning and understanding optimal class sizes.",
                businessRules: [
                    "Positive integer value",
                    "Represents total attendees per class",
                    "Used in capacity analysis",
                    "Helps determine future class sizing"
                ]
            },
            {
                type: "column",
                name: "known_category",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.known_class_category",
                description: "Category or type of Known class (e.g., New Members, Next Steps, Volunteer Orientation)",
                owner: "Data Insights Team",
                examples: ["New Members", "Next Steps", "Volunteer Orientation", "Ministry Connection"],
                usage: "Classifies the type of Known event. Important for segmenting different engagement paths and ministry funnels.",
                businessRules: [
                    "Limited to predefined categories",
                    "Determines follow-up pathway",
                    "Used for category-specific reporting",
                    "Links to specific ministry teams"
                ]
            },
            {
                type: "column",
                name: "known_next_step",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.known_next_step",
                description: "The recommended or assigned next step for the attendee following their Known class participation",
                owner: "Data Insights Team",
                examples: ["Join Small Group", "Attend Baptism Class", "Serve Orientation", "Ministry Team Meeting", "One-on-One with Pastor"],
                usage: "Guides attendee journey through discipleship path. Critical for follow-up communication and tracking progression.",
                businessRules: [
                    "Contains actionable next step description",
                    "May be auto-assigned or pastor-selected",
                    "Used in follow-up communications",
                    "Tracks progression through discipleship funnel"
                ]
            },
            {
                type: "column",
                name: "known_step_note",
                viewName: "known_step_view",
                dataType: "STRING",
                source: "docs.columns.known_step_note",
                description: "Additional notes, comments, or context about the Known event step, often added by pastors or coordinators",
                owner: "Data Insights Team",
                examples: ["Interested in volunteering with kids", "Has questions about baptism", "Prefers email contact", "New to area, looking for community"],
                usage: "Provides qualitative context for follow-up. Essential for personalized pastor engagement and understanding attendee needs.",
                businessRules: [
                    "Free-text field",
                    "May be null if no additional context",
                    "Used by pastors for follow-up preparation",
                    "Contains sensitive pastoral information"
                ]
            }
        ];

        const searchInput = document.getElementById('searchInput');
        const resultsDiv = document.getElementById('results');
        const resultsCount = document.getElementById('resultsCount');

        function createViewCard(contract, isExpanded = false) {
            const detailsId = `details-view-${contract.name}`;
            
            return `
                <div class="contract-card view-card ${isExpanded ? 'expanded' : ''}" onclick="toggleDetails('${detailsId}', this)">
                    <div class="contract-header">
                        <div class="contract-name">
                            📊 ${contract.name}
                            <span class="contract-badge">VIEW</span>
                        </div>
                        <span class="toggle-icon">▼</span>
                    </div>
                    
                    <div class="contract-description">${contract.description}</div>
                    
                    <div class="contract-meta">
                        <div class="meta-item">
                            <div class="meta-label">Database</div>
                            <div class="meta-value">${contract.database}</div>
                        </div>
                        <div class="meta-item">
                            <div class="meta-label">Schema</div>
                            <div class="meta-value">${contract.schema}</div>
                        </div>
                        <div class="meta-item">
                            <div class="meta-label">Owner</div>
                            <div class="meta-value">${contract.owner}</div>
                        </div>
                        <div class="meta-item">
                            <div class="meta-label">Total Columns</div>
                            <div class="meta-value">${contract.columns.length}</div>
                        </div>
                    </div>
                    
                    <div class="contract-details ${isExpanded ? 'visible' : ''}" id="${detailsId}">
                        <div class="detail-section">
                            <div class="detail-title">🔑 Data Quality Assertions</div>
                            <div class="detail-content">
                                <ul class="rules-list">
                                    <li><strong>Unique Key:</strong> ${contract.uniqueKey.join(', ')}</li>
                                    <li><strong>Non-Null Fields:</strong> ${contract.nonNull.join(', ')}</li>
                                </ul>
                            </div>
                        </div>
                        
                        <div class="detail-section">
                            <div class="detail-title">📋 All Columns</div>
                            <table class="columns-table">
                                <thead>
                                    <tr>
                                        <th>Column Name</th>
                                        <th>Source</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    ${contract.columns.map(col => `
                                        <tr>
                                            <td><code>${col}</code></td>
                                            <td>docs.columns.*</td>
                                        </tr>
                                    `).join('')}
                                </tbody>
                            </table>
                        </div>
                        
                        <div class="detail-section">
                            <div class="detail-title">🏷️ Tags</div>
                            <div class="detail-content">
                                ${contract.tags.map(tag => `<span style="background: #f0f0ff; padding: 5px 12px; border-radius: 15px; margin-right: 8px; display: inline-block;">${tag}</span>`).join('')}
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }

        function createColumnCard(contract, isExpanded = false) {
            const detailsId = `details-${contract.name}`;
            
            return `
                <div class="contract-card ${isExpanded ? 'expanded' : ''}" onclick="toggleDetails('${detailsId}', this)">
                    <div class="contract-header">
                        <div class="contract-name">
                            ${contract.name}
                            <span class="contract-badge">${contract.dataType}</span>
                        </div>
                        <span class="toggle-icon">▼</span>
                    </div>
                    
                    <div class="contract-description">${contract.description}</div>
                    
                    <div class="contract-meta">
                        <div class="meta-item">
                            <div class="meta-label">View</div>
                            <div class="meta-value">${contract.viewName}</div>
                        </div>
                        <div class="meta-item">
                            <div class="meta-label">Data Type</div>
                            <div class="meta-value">${contract.dataType}</div>
                        </div>
                        <div class="meta-item">
                            <div class="meta-label">Source</div>
                            <div class="meta-value">${contract.source}</div>
                        </div>
                        ${contract.assertions ? `
                        <div class="meta-item">
                            <div class="meta-label">Assertions</div>
                            <div class="meta-value">${contract.assertions}</div>
                        </div>
                        ` : ''}
                    </div>
                    
                    <div class="contract-details ${isExpanded ? 'visible' : ''}" id="${detailsId}">
                        <div class="detail-section">
                            <div class="detail-title">💡 How It's Used</div>
                            <div class="detail-content">${contract.usage}</div>
                        </div>
                        
                        <div class="detail-section">
                            <div class="detail-title">📝 Example Values</div>
                            <div class="examples-grid">
                                ${contract.examples.map(ex => `<div class="example-item">${ex}</div>`).join('')}
                            </div>
                        </div>
                        
                        <div class="detail-section">
                            <div class="detail-title">⚖️ Business Rules</div>
                            <ul class="rules-list">
                                ${contract.businessRules.map(rule => `<li>${rule}</li>`).join('')}
                            </ul>
                        </div>
                    </div>
                </div>
            `;
        }

        function toggleDetails(detailsId, cardElement) {
            const details = document.getElementById(detailsId);
details.classList.toggle('visible');
cardElement.classList.toggle('expanded');
function search(query) {
        const lowerQuery = query.toLowerCase().trim();
        
        if (!lowerQuery) {
            displayAll();
            return;
        }

        const exactMatches = dataContracts.filter(item => 
            item.name.toLowerCase() === lowerQuery
        );

        const partialMatches = dataContracts.filter(item => 
            item.name.toLowerCase().includes(lowerQuery) && 
            item.name.toLowerCase() !== lowerQuery
        );

        const matches = [...exactMatches, ...partialMatches];

        if (matches.length === 0) {
            resultsDiv.innerHTML = `
                <div class="no-results">
                    <div class="no-results-icon">🔍</div>
                    <h3>No contracts found matching "${query}"</h3>
                    <p>Try: known_step_view, campus, rms_person_id, known_step_status</p>
                </div>
            `;
            return;
        }

        resultsDiv.innerHTML = matches.map(item => {
            if (item.type === 'view') {
                return createViewCard(item, matches.length === 1);
            } else {
                return createColumnCard(item, matches.length === 1);
            }
        }).join('');
    }

    function displayAll() {
        const views = dataContracts.filter(item => item.type === 'view');
        const columns = dataContracts.filter(item => item.type === 'column');
        
        resultsDiv.innerHTML = `
            ${views.map(view => createViewCard(view, false)).join('')}
            ${columns.map(col => createColumnCard(col, false)).join('')}
        `;
    }

    searchInput.addEventListener('input', (e) => {
        search(e.target.value);
    });

    window.toggleDetails = toggleDetails;

    displayAll();
</script>
```html
