# Sometimes it's a README fix, or something like that - which isn't relevant for
# including in a project's CHANGELOG for example
declared_trivial = github.pr_title.include? "#trivial"

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

kotlin_detekt.report_file = "build/reports/detekt/detekt.xml"
kotlin_detekt.gradle_task = "detektAll"
kotlin_detekt.detekt

junit_tests_dir = "purchases/build/reports/**/*.xml"
Dir[junit_tests_dir].each do |file_name|
  junit.parse file_name
  junit.show_skipped_tests = true
  junit.report
end

all_source_files = danger.git.modified_files + danger.git.added_files

changelog_changed = all_source_files.include?("CHANGELOG.md")
is_trivial = danger.github.pr_title.include?("#trivial")

warn("Any changes to library code should be reflected in the Changelog.\n\nPlease consider adding a note there.") if (!is_trivial && !changelog_changed)

lgtm.check_lgtm 